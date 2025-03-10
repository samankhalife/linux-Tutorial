# crushtool
`crushtool` is a utility in Ceph used to interact with **CRUSH (Controlled Replication Under Scalable Hashing)** maps. CRUSH is the algorithm Ceph uses to determine how data is distributed and stored across the cluster. The `crushtool` provides various commands to create, decompile, compile, and analyze CRUSH maps, which control how Ceph places data onto OSDs based on failure domains, weights, and replication rules.



## Common `crushtool` Commands and Subcommands

### 1. **decompile**
Decompiles a binary CRUSH map into a human-readable text format.

```bash
crushtool --decompile <binary-crush-map> -o <output-text-file>
```

- Example:
  ```bash
  crushtool --decompile /etc/ceph/crushmap -o crushmap.txt
  ```

This command takes the binary CRUSH map `/etc/ceph/crushmap` and decompiles it into the human-readable file `crushmap.txt`.

### 2. **compile**
Compiles a text-format CRUSH map into a binary format that Ceph uses.

```bash
crushtool --compile <input-text-file> -o <output-binary-crush-map>
```

- Example:
  ```bash
  crushtool --compile crushmap.txt -o /etc/ceph/crushmap
  ```

This command compiles the human-readable `crushmap.txt` into the binary CRUSH map `/etc/ceph/crushmap`.

### 3. **show**
Displays the contents of a compiled CRUSH map in a more readable format directly in the terminal without decompiling it into a separate file.

```bash
crushtool --show <binary-crush-map>
```

- Example:
  ```bash
  crushtool --show /etc/ceph/crushmap
  ```

This command prints the contents of the binary CRUSH map in a readable format.

### 4. **analyze**
Analyzes how data will be distributed according to a given CRUSH map. You can use it to simulate data placement and failure domains.

```bash
crushtool --analyze <binary-crush-map> --rule <rule-id> --type <type-name> --num-rep <num-replicas>
```

- Example:
  ```bash
  crushtool --analyze /etc/ceph/crushmap --rule 0 --type osd --num-rep 3
  ```

This command simulates data placement using the CRUSH map's rule 0, distributing replicas across OSDs with a replication factor of 3.

### 5. **test**
Tests how a specific CRUSH map distributes data for a particular bucket or item, allowing administrators to verify placement behavior.

```bash
crushtool --test --rule <rule-id> --num-rep <num-replicas> --show-mappings --show-utilization --output-csv <output-file> <binary-crush-map>
```

- Example:
  ```bash
  crushtool --test --rule 0 --num-rep 3 --show-mappings /etc/ceph/crushmap
  ```

This command tests the distribution of data according to rule 0 with 3 replicas and displays the placement mappings for the current CRUSH map.

### 6. **reweight**
Reweights the CRUSH map’s OSDs or buckets based on a new weight, adjusting the distribution of data.

```bash
crushtool --reweight-item <item-name> --weight <new-weight> -i <input-crush-map> -o <output-crush-map>
```

- Example:
  ```bash
  crushtool --reweight-item osd.0 --weight 0.8 -i /etc/ceph/crushmap -o new-crushmap
  ```

This command reweights `osd.0` to 0.8 in the CRUSH map.

### 7. **add-bucket**
Adds a new bucket to the CRUSH map. Buckets define failure domains such as racks, hosts, and OSDs.

```bash
crushtool --add-bucket <bucket-name> <bucket-type> -i <input-crush-map> -o <output-crush-map>
```

- Example:
  ```bash
  crushtool --add-bucket rack0 rack -i /etc/ceph/crushmap -o new-crushmap
  ```

This command adds a new bucket named `rack0` of type `rack` to the CRUSH map.

### 8. **set-item-class**
Assigns a class to an item (such as an OSD) in the CRUSH map. Ceph uses classes to differentiate between storage types (e.g., SSD, HDD).

```bash
crushtool --set-item-class <class> <item-name> -i <input-crush-map> -o <output-crush-map>
```

- Example:
  ```bash
  crushtool --set-item-class ssd osd.1 -i /etc/ceph/crushmap -o new-crushmap
  ```

This command sets `osd.1` to belong to the `ssd` class.

### 9. **rm-bucket**
Removes a bucket from the CRUSH map.

```bash
crushtool --rm-bucket <bucket-name> -i <input-crush-map> -o <output-crush-map>
```

- Example:
  ```bash
  crushtool --rm-bucket rack0 -i /etc/ceph/crushmap -o new-crushmap
  ```

This command removes the bucket `rack0` from the CRUSH map.

### 10. **rm-item**
Removes an item (such as an OSD) from the CRUSH map.

```bash
crushtool --rm-item <item-name> -i <input-crush-map> -o <output-crush-map>
```

- Example:
  ```bash
  crushtool --rm-item osd.0 -i /etc/ceph/crushmap -o new-crushmap
  ```

This command removes `osd.0` from the CRUSH map.

### 11. **move**
Moves a bucket to a different location in the hierarchy of the CRUSH map.

```bash
crushtool --move <bucket-name> <new-location> -i <input-crush-map> -o <output-crush-map>
```

- Example:
  ```bash
  crushtool --move host1 rack1 -i /etc/ceph/crushmap -o new-crushmap
  ```

This command moves the bucket `host1` to `rack1`.

### 12. **tree**
Prints the CRUSH map hierarchy in a tree-like format.

```bash
crushtool --tree <binary-crush-map>
```

- Example:
  ```bash
  crushtool --tree /etc/ceph/crushmap
  ```

This command displays the hierarchy of the CRUSH map, showing how OSDs, hosts, racks, etc., are organized.



## Typical Use Cases:

1. **Customizing Data Placement:**
   Ceph admins use `crushtool` to modify CRUSH maps for fine-tuned control over how data is replicated and distributed across failure domains (e.g., racks, hosts, OSDs).

2. **Simulating Data Distribution:**
   With commands like `analyze` and `test`, admins can simulate how CRUSH maps will distribute data across the cluster, ensuring even utilization and high availability.

3. **Reweighting for Performance:**
   Using `reweight`, admins can adjust the weights of OSDs or other CRUSH components to ensure even distribution of data, optimizing performance and capacity usage.

4. **Failure Domain Management:**
   By adding and removing buckets, Ceph administrators can redefine failure domains like hosts and racks, ensuring the cluster's resilience against hardware failures.

5. **Storage Tiering with Classes:**
   Assigning items to classes (e.g., SSDs or HDDs) allows for storage tiering, where Ceph can manage fast storage devices (SSDs) differently from slower ones (HDDs).



## Conclusion

The `crushtool` is an essential utility for managing and customizing CRUSH maps in a Ceph cluster. It offers various commands for creating, compiling, testing, and analyzing CRUSH maps, giving administrators the ability to define and optimize how Ceph distributes and replicates data across the cluster. Through `crushtool`, failure domains, replication rules, and storage tiers can be efficiently controlled, providing resilience and performance to the Ceph cluster.
