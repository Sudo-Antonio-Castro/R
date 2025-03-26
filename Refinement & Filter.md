# Refinement & Filter


**Video Pending**


### Overview
This project focuses on processing a CSV file focused on two columns:
- **Resource**: Identifies different sections.
- **Attempts**: Tracks the number of attempts for each resource.

The goal is to:
1. Retain resources that were **not attempted** (value of 0 in the Attempts column).
2. Remove resource with **attempts greater than 0**.
3. Filter and keep only specific resource within a defined range.

### Walkthrough using RGui

1. **Install 'stringr' Package**
   ```R
   install.packages("stringr")
   ```
2. **Load 'stringr'**
   ```R
   library(stringr)
   ```
4. **Load CSV**
   ```R
   df <- read.csv(file.choose())
   ```
6. Filter **Attempts** to keep rows with a value of **0**
   ```R
   df <- df[df$Attempts == 0, ]
   ```
8. **Extract Resource**
   - Only care about the two numbers before the second period (1.1.1, 1.1.2, to 1.1)
   ```R
   df$Resource_prefix <- str_extract(df$Resource, "^[0-9]+\\.[0-9]+")
   ```
10. **Defined Valid Range**
    - Only want specific sections.
    ```R
    valid_ranges <- c("1.1", "4.2", "7.7", "14.8", "14.9", "14.11", sprintf("2.%d", 5:7), sprintf("3.%d", 1:14), sprintf("5.%d", c(1:4, 7:9)), sprintf("6.%d", 2:4), sprintf("10.%d", 1:3), sprintf("11.%d", c(1:5, 7, 9)), sprintf("12.%d", 1:7), sprintf("13.%d", 1:4))
    ```
12. **Filter by valid range**
    ```R
    df <- df[df$Resource_prefix %in% valid_ranges, ]
    ```
14. **Time to save!**
    ```R
    write.csv(df, "Missing Homework.csv", row.names = FALSE)
    ```

**Commands**
