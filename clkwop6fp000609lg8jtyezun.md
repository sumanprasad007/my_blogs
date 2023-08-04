---
title: "Day 5 :  Automating Log Analysis with Bash Script - Step-by-Step Guide 📝"
datePublished: Fri Aug 04 2023 14:31:35 GMT+0000 (Coordinated Universal Time)
cuid: clkwop6fp000609lg8jtyezun
slug: day-5-automating-log-analysis-with-bash-script-step-by-step-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691159260842/9907750e-8343-41f5-890b-edcc23d6278a.png
tags: linux, developer, devops, shell, 90daysofdevops

---

# **📍 Introduction:**

Hey there, DevOps enthusiasts! Are you tired of manually analyzing log files and generating reports every day? Well, worry no more! In this blog, we will walk you through a simple yet powerful Bash script that automates the process of log analysis and report generation. 🚀

### **🔍 Challenge Overview**

You are a system administrator managing a network of servers, and every day, log files are generated on each server containing important system events and error messages. Your daily task is to analyze these log files, identify specific events, and generate a summary report.

### **🔍 Introducing the Log Analyzer and Report Generator 📊**

The Bash script we will create automates the following steps:

1. **Input**: The script takes the path to the log file as a command-line argument.
    
2. **Error Count**: It analyzes the log file and counts the number of error messages. An error message can be identified by keywords like "ERROR" or "Failed," and it prints the total error count.
    
3. **Critical Events**: The script searches for lines containing the keyword "CRITICAL" and prints those lines along with the line number.
    
4. **Top Error Messages**: It identifies the top 5 most common error messages and displays them along with their occurrence count.
    
5. **Summary Report**: The script generates a summary report in a separate text file, including the date of analysis, log file name, total lines processed, total error count, top 5 error messages, and list of critical events with line numbers.
    

### **📄 Script Implementation**

Below is the complete Bash script to automate the log analysis and report generation. We will go through it step-by-step:

```plaintext
#!/bin/bash

# Check if the log file path and title are provided as arguments
if [ $# -lt 1 ]; then
  echo "Error: Please provide the path to the log file as an argument."
  echo "Usage: $0 <path_to_log_file>"
  exit 1
fi

# Check if the log file exists
log_file="$1"
if [ ! -f "$log_file" ]; then
  echo "Error: The provided log file does not exist."
  exit 1
fi

# Function to print the summary report
print_summary_report() {
  echo "Date of analysis: $(date)"
  echo "Log file name: $log_file"
  echo "Total lines processed: $total_lines"
  echo "Total error count: $total_error_count"

  echo -e "\nTop 5 error messages with their occurrence count:"
  for error_msg in "${!error_counts[@]}"; do
    echo "$error_msg: ${error_counts[$error_msg]}"
  done

  echo -e "\nCritical Events (Line Number: Event):"
  for line_num in "${!critical_events[@]}"; do
    echo "$line_num: ${critical_events[$line_num]}"
  done
}

# Initialize variables
total_lines=0
total_error_count=0
declare -A error_counts
declare -A critical_events

# Analyzing the log file
while IFS= read -r line; do
  ((total_lines++))

  # Count error messages
  if grep -q -E 'ERROR|Failed' <<< "$line"; then
    ((total_error_count++))
    for keyword in "ERROR" "Failed"; do
      if grep -q -w "$keyword" <<< "$line"; then
        ((error_counts["$keyword"]++))
      fi
    done
  fi

  # Search for critical events and store them with line numbers
  if grep -q -w "CRITICAL" <<< "$line"; then
    critical_events["$total_lines"]="$line"
  fi
done <"$log_file"

# Get the top 5 error messages
top_5_errors=$(printf "%s\n" "${!error_counts[@]}" | sort -n -k2 -r | head -n 5)

# Generate the summary report in a separate file with auto-generated name
title="Log_Analysis_Summary"
summary_file="${title}_$(date +'%Y-%m-%d_%H-%M-%S').txt"
print_summary_report >"$summary_file"

# Print the summary report to the terminal
cat "$summary_file"

# Optional Enhancement: Move processed log file to a designated directory
archive_directory="archive"
if [ ! -d "$archive_directory" ]; then
  mkdir "$archive_directory"
fi

archive_file="${archive_directory}/$(date +'%Y-%m-%d_%H-%M-%S')_${log_file}"
cp "$log_file" "$archive_file"

echo "Log file archived to: $archive_file"
```

### **🔍 Step-by-Step Explanation**

1. **Checking Arguments**: The script checks if the log file path and title are provided as arguments. If not, it displays an error message and usage instructions.
    
2. **Log File Existence Check**: It checks if the provided log file exists. If not, it shows an error and exits.
    
3. **Summary Report Function**: We define a function `print_summary_report()` to print the analysis summary in the terminal.
    
4. **Variable Initialization**: The script initializes variables for counting total lines, total error count, and associative arrays for error counts and critical events.
    
5. **Log File Analysis**: The script reads the log file line by line, counting errors, and finding critical events.
    
6. **Top Error Messages**: The script finds the top 5 most common error messages using associative arrays and sorting.
    
7. **Generating Summary Report**: The script generates the summary report in a separate file with an auto-generated name containing the title, date, and time.
    
8. **Optional Enhancement**: The script moves the processed log file to a designated directory with a timestamp.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691159408789/6a5d570d-dae7-47f3-a9a0-828552e01950.png align="center")

### **🔍 Execution Steps**

Follow these steps to execute the Log Analyzer and Report Generator:

1. **Prepare the Log File**: Place the log file you want to analyze in the same directory as the script. In this example, we'll use `sample_log.log`.
    
2. **Make Script Executable**: Ensure the script has execution permissions by running `chmod +x log_analyzer.sh`.
    
3. **Run the Script**: Execute the script with the log file path as an argument and an optional title:
    
    ```plaintext
    /log_analyzer.sh sample_log.log 
    ```
    
4. **Observe the Results**: The script will process the log file, print the summary report in the terminal, and generate a log summary file with an auto-generated name (e.g., `Log_Analysis_Summary_2023-08-04_10-15-23.txt`).
    

**Archive Log Files**: Optionally, the script archives the processed log file in the `archive` directory.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691159459352/316fa940-32cb-499d-a837-d1ece674e3a7.png align="center")

# **📍 Conclusion**

You've just created an efficient and time-saving Bash script to automate log analysis and report generation. With this script, you can now easily manage your network of servers and gain insights from log data without hassle. Happy automating! 🎉

### **🔍 Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690656559825/0474ff76-1d75-4ce0-93ea-1194d2444f74.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

### **🔍 Check out my YouTube channel - Prasad Suman Mohan:**

🔗 [**youtube.com/@sumanprasad007**](http://youtube.com/@sumanprasad007)

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690893614276/e567a0e4-c76d-4f49-b537-34ca8e727e5d.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")](https://www.youtube.com/@sumanprasad007)