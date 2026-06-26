Markdown
# CyLab Security Academy: Log Hunt Challenge

A write-up and solution for the **Log Hunt** (Easy, 50 pts) forensic/general skills challenge on CyLab Security Academy.

## Challenge Description
> "Our server seems to be leaking pieces of a secret flag in its logs. The parts are scattered and sometimes repeated. Can you reconstruct the original flag?"

**Hints provided:**
1. You can use `grep` to filter only matching lines from the log.
2. Some lines are duplicates; ignore extra occurrences.

## Solution Walkthrough

The challenge provides a standard log file (`server.log`). To isolate the flag efficiently without parsing thousands of entries manually, we can leverage a powerful Linux command-line pipeline.

### Step 1: Open Terminal and Navigate to the Log File
First, open your terminal and change directories to where the file was downloaded (e.g., the `Downloads` directory):
```bash
cd ~/Downloads

### Step 2: Extract and De-duplicate the Flag Fragments
Run the following pipeline to search for the keyword, sort the results, and remove all duplicate noise:

Bash
grep -i "flag" server.log | sort | uniq
Command Breakdown:
grep -i "flag": Case-insensitively searches the log file for lines containing "flag".

sort: Alphabetically sorts the matching log lines (a required prerequisite for the uniq command to work effectively).

uniq: Discards consecutive duplicate lines, leaving only unique instances of the flag pieces.

### Step 3: Analyze the Output
Running the pipeline yields the following clean output tracking the flag segments chronologically:

Plaintext
[1990-08-09 10:00:10] INFO FLAGPART: picoCTF{us3_
[1990-08-09 10:02:55] INFO FLAGPART: y0urlinux_
[1990-08-09 10:05:54] INFO FLAGPART: sk1lls_
[1990-08-09 10:10:54] INFO FLAGPART: cedfa5fb}
Final Flag
By concatenating the unique fragments in chronological order, we get the complete flag:

Plaintext
picoCTF{us3_y0urlinux_sk1lls_cedfa5fb}
