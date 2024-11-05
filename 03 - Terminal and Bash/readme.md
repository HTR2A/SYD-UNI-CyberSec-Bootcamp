# Lucky Duck Casino - Terminal and Bash Investigation Report

## Overview
The following report outlines the findings from the investigation into losses incurred at the Lucky Duck Casino. The objective was to identify a rogue player and dealer suspected of colluding to scam the casino out of thousands of dollars. The analysis focused on the activities at the roulette tables on specific days when significant losses were noted.

### Directories Setup
To organize the investigation, the following directories were created:
- **Lucky_Duck_Investigations** (main directory)
  - **Roulette_Loss_Investigation**
    - **Player_Analysis**: Analyzed player activities.
    - **Dealer_Analysis**: Analyzed dealer activities.
    - **Player_Dealer_Correlation**: Summarized findings about possible collusion.


---

## Step-by-Step Investigation

### Step 1: Gathering Evidence
The investigation centered around the large losses that occurred on March 10, 12, and 15. Evidence files were downloaded and relevant schedules and player data were moved to their respective analysis directories:
- **Dealer Schedules** (from March 10, 12, and 15) were moved to the **Dealer_Analysis** directory.
- **Roulette Player Win/Loss Data** (from March 10, 12, and 15) were moved to the **Player_Analysis** directory.

### Step 2: Player Analysis
Using `grep`, all losses from the roulette tables were isolated for the dates of March 10, 12, and 15. The following key observations were recorded in the **Notes_Player_Analysis.txt** file:
- Losses occurred at specific times across the three days, involving a particular player named Mylie Schmidt.
- **Total Count of Times Played**: Mylie Schmidt was identified as the main player involved during each of the times the losses occurred.

**Roulette Losses Summary** (as per **Roulette_Losses.txt**):
```
0310_win_loss_player_data.txt:05:00:00 AM -$82,348 Amirah Schneider, Nola Portillo, Mylie Schmidt, Suhayb Maguire, Millicent Betts, Avi Graves
0310_win_loss_player_data.txt:08:00:00 AM -$97,383 Chanelle Tapia, Shelley Dodson, Valentino Smith, Mylie Schmidt
0310_win_loss_player_data.txt:02:00:00 PM -$82,348 Jaden Clarkson, Kaidan Sheridan, Mylie Schmidt
0310_win_loss_player_data.txt:08:00:00 PM -$65,348 Mylie Schmidt, Trixie Velasquez, Jerome Klein, Rahma Buckley
0310_win_loss_player_data.txt:11:00:00 PM -$88,383 Mcfadden Wasim, Norman Cooper, Mylie Schmidt
0312_win_loss_player_data.txt:05:00:00 AM -$182,300 Montana Kirk, Alysia Goodman, Halima Little, Etienne Brady, Mylie Schmidt
0312_win_loss_player_data.txt:08:00:00 AM -$97,383 Rimsha Gardiner, Fern Cleveland, Mylie Schmidt, Kobe Higgins
0312_win_loss_player_data.txt:02:00:00 PM -$82,348 Mae Hail, Mylie Schmidt, Ayden Beil
0312_win_loss_player_data.txt:08:00:00 PM -$65,792 Tallulah Rawlings, Josie Dawe, Mylie Schmidt, Hakim Stott, Esther Callaghan, Ciaron Villanueva
0312_win_loss_player_data.txt:11:00:00 PM -$88,229 Vlad Hatfield, Kerys Frazier, Mya Butler, Mylie Schmidt, Lex Oakley, Elin Wormald
0315_win_loss_player_data.txt:05:00:00 AM -$82,844 Arjan Guzman, Sommer Mann, Mylie Schmidt
0315_win_loss_player_data.txt:08:00:00 AM -$97,001 Lilianna Devlin, Brendan Lester, Mylie Schmidt, Blade Robertson, Derrick Schroeder
0315_win_loss_player_data.txt:02:00:00 PM -$182,419 Mylie Schmidt, Corey Huffman
```

### Step 3: Dealer Analysis
Using `awk` and `grep`, I isolated the dealer schedule during each time a significant loss occurred. The analysis showed:
- **Dealer Working During Losses**: Billy Jones was the dealer during each of the times when major losses were recorded.
- **Number of Times Dealer Worked During Losses**: Billy Jones was the only roulette dealer present for all 13 occurrences of major losses.

Details were documented in the **Notes_Dealer_Analysis.txt** file:
```
Billy Jones was the only Roulette Dealer that worked all 13 times when a loss occurred.
```

**Dealers Working During Losses** (as per **Dealers_working_during_losses.txt**):
```
05:00:00 AM Billy Jones
08:00:00 AM Billy Jones
02:00:00 PM Billy Jones
08:00:00 PM Billy Jones
11:00:00 PM Billy Jones
...
```

### Step 4: Correlating Player and Dealer
Based on the combined player and dealer analysis, it was concluded that:
- **Player**: Mylie Schmidt
- **Dealer**: Billy Jones
- These two individuals were consistently involved in each instance of the casino's significant losses.

The correlation was documented in the **Notes_Player_Dealer_Analysis.txt** file:
```
We determined that Mylie Schmidt and Billy Jones worked together to rip off the casino in the 13 instances that they both played and worked at the roulette game.
```

---

## Script Development
To streamline future investigations, the following shell script was created:

### `roulette_dealer_finder_by_time.sh`
This script allows quick identification of the dealer working at a specific time for future loss events.

**Code**:
```bash
#!/bin/bash

cat $1_Dealer_schedule.txt | awk -F" " '{print $1, $2, $5, $6}' | grep "$2"
```

**Usage**:
- **Arguments**: Date (e.g., `0310`), Time (e.g., `05:00:00 AM`).
- **Example**: To find the dealer working on March 10 at 5:00 AM:
  ```
  ./roulette_dealer_finder_by_time.sh 0310 "05:00:00 AM"
  ```

---

## Summary of Findings
The investigation into losses at the Lucky Duck Casino identified collusion between player Mylie Schmidt and dealer Billy Jones. The evidence showed:
- Billy Jones was the dealer working during all times that major losses were recorded.
- Mylie Schmidt was consistently playing during those times, leading to the conclusion that they were colluding to scam the casino.

### Recommendations
- **Enhanced Monitoring**: Implement stricter monitoring of both players and dealers, especially during large winnings or losses.
- **Employee Background Checks**: Perform thorough background checks on all dealers.
- **Randomized Dealer Assignments**: Randomize dealer assignments to games to prevent prolonged interaction between any one dealer and player.

---

## Files Submitted
The following files were moved to the **Player_Dealer_Correlation** directory and compressed for submission:
- **Notes_Player_Analysis.txt**
- **Notes_Dealer_Analysis.txt**
- **Notes_Player_Dealer_Analysis.txt**
- **Roulette_Losses.txt**
- **Dealers_working_during_losses.txt**
- **roulette_dealer_finder_by_time.sh**

