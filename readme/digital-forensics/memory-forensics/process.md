---
icon: arrow-progress
---

# Process

## Memory Forensics Process

1. **Memory Acquisition**:
   * **What it is**: Capturing the physical RAM of a system running malware.
   * **How to do it**: Use tools like Dumpit from the Comae memory toolkit. This tool is easy to use, fast, and free. You can dump memory in different formats, including Microsoft crash dumps.
   * **Key Points**:
     * Run the malware in your environment.
     * Use Dumpit to capture the memory.
     * For large RAM systems, use compression options to speed up the process.\

2. **Memory Analysis**:
   * **What it is**: Analyzing the captured memory to extract malware artifacts.
   * **Steps**:
     * After capturing the memory, analyze it to identify and extract malware-related data.
     * This helps in understanding the behavior and impact of the malware.

