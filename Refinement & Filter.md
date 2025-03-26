# Refinement & Filter


**Video Pending**


I have a CSV file with Column 1 being **Resource** and Column 2 being **Attempts**.

I am looking to keep Resources that were not attempted, and remove rows with a value greater than **0**

Finally, I only want specific sections (Resources within range)

### Walkthrough RGui

1. Begin by installing 'stringr' ```install.packages("stringr")```
2. Load 'stringr' ```library(stringr)```
3. Load CSV ```df <- read.csv(file.choose())```
4. Filter **Attempts** to keep rows with a value of **0** ```df <- df[df$Attempts == 0, ]```
5. Because resources has 1.1.1 - 1.1.2, I only care about the two numbers before the second period <br> ```df$Resource_prefix <- str_extract(df$Resource, "^[0-9]+\\.[0-9]+")```
6. I have specific ranges to keep: <br> ```valid_ranges <- c("1.1", "4.2", "7.7", "14.8", "14.9", "14.11", sprintf("2.%d", 5:7), sprintf("3.%d", 1:14), sprintf("5.%d", c(1:4, 7:9)), sprintf("6.%d", 2:4), sprintf("10.%d", 1:3), sprintf("11.%d", c(1:5, 7, 9)), sprintf("12.%d", 1:7), sprintf("13.%d", 1:4))```
7. Now filter by range <br> ```df <- df[df$Resource_prefix %in% valid_ranges, ]```
8. Save! ```write.csv(df, "Missing Homework.csv", row.names = FALSE)```

**Commands**
