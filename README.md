Google Ads Script: Auto-Exclude Keywords with Over 100 Impressions and No Clicks

Overview
This script for Google Ads automates the process of identifying and excluding search terms that have generated over 100 impressions but no clicks. It helps optimize ad spend by preventing ads from appearing for search terms that don't lead to engagement. The script adds these terms as exact match negative keywords to a specific negative keyword list in your Google Ads account.

Features
Keyword Analysis: Identifies search terms with over 100 impressions but zero clicks.
Negative Keyword List Management: Checks if a specific negative keyword list exists and creates one if it doesn't.
Exact Match Exclusion: Adds the identified search terms as exact match negative keywords to the list.

How It Works
Data Querying: The script queries the search_term_view to find search terms with ≥100 impressions and 0 clicks.
List Verification: It checks for the existence of a negative keyword list named "Keywords über 100 Impressionen ohne Klicks" (Keywords with over 100 Impressions and No Clicks). If the list doesn't exist, the script creates it.
Keyword Addition: Each identified search term is added as an exact match negative keyword to the specified list.

Usage
This script can be scheduled to run regularly in your Google Ads account to continuously update the negative keyword list.
Ensure that the name of the negative keyword list in the script matches the one in your Google Ads account or adjust accordingly.
It is recommended to review the list periodically to ensure relevance and accuracy.

Customization
The script can be modified to change the impressions threshold or to apply different criteria for keyword exclusion.
It can also be adjusted to work with different types of campaigns or to manage multiple lists.
