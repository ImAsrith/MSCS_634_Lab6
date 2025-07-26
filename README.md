# MSCS 634 Lab 6: Association Rule Mining with Apriori and FP-Growth

## Purpose
This lab applies frequent itemset mining and association rule analysis to a retail basket dataset. The notebook prepares and cleans transactional data, discovers frequent itemsets using Apriori and FP Growth with the same thresholds, generates rules with support, confidence, and lift, and uses Seaborn visualizations to interpret patterns. A short comparison explains which algorithm was faster and why.

## Dataset
UCI Machine Learning Repository, Online Retail. If the link is blocked, the notebook loads the Excel file directly from UCI or from a local copy. Columns used include InvoiceNo, Description, Quantity, InvoiceDate, UnitPrice, CustomerID, and Country.

## Method and settings
Data cleaning removed credit invoices, rows with missing item names, and rows with non-positive quantity or unit price. Items were normalized with stripped text. A one-hot invoice by item basket was built with dtype uint8 to control memory. The same thresholds were used for both algorithms to allow a fair comparison.

Key parameters for the reported run:
- Invoices: 19,872
- Items: 2,858
- Basket size and memory: 19,872 by 2,858, about 54.3 MB
- Minimum support: 0.02
- Maximum itemset length: 2
- Minimum confidence for rules: 0.50

## Visualizations
The notebook includes a bar plot of the most frequent items, a co-occurrence heatmap for popular items, bar plots of the top frequent itemsets by support for each algorithm, and scatter plots of confidence versus lift for the generated rules.

## Results
Both algorithms produced identical frequent itemsets and rules at the shared thresholds.
- Apriori itemsets: 378 in 0.67 seconds
- FP Growth itemsets: 378 in 11.99 seconds
- Association rules: 49 from each method at confidence 0.50

## Comparative analysis
Apriori was faster than FP-Growth in this configuration. The search was limited to pairs, which allows Apriori to count candidate pairs efficiently. FP Growth builds and traverses a prefix tree, which adds overhead that does not pay off when the search depth is short and support is moderate. With longer itemsets or lower support, FP Growth often becomes faster.

## Challenges and resolutions
Initial attempts with low support or very small country subsets produced an explosion of patterns or trivial rules. This was resolved by using an adaptive and realistic support level, limiting maximum itemset length to pairs for stability, and building the basket with a compact dtype. Memory stayed within Colab limits and all cells ran to completion.

