# 📝 Challenge Write-up: YOU SNOZE YOU LOZE

| Attribute | Details |
| :--- | :--- |
| **Event** | TexSAW 2026 |
| **Category** | OSINT |
| **Difficulty** | Easy / Medium |
| **Target File** | `20260124_...` (Image File) |
| **Points** | 100 |

## 1. The Challenge Scenario
The challenge provided a high-action race photo taken at night with the filename `20260124_...`. The accompanying narrative gave a crucial hint: *"D'oh, I overslept and missed most of the race! But wait, my friend took a picture while I was out, but I can't tell whose in the lead. Can you help me figure out the two cars that are in the lead? Usually they like to twin around this time of night..."* The objective was to identify the exact race, determine the two leading vehicles based on the event's timeline, and submit their identifying numbers in the specified format.

## 2. The Step-by-Step Solution
Instead of manually identifying the vehicles by squinting at blurry racing numbers, I utilized a streamlined Reverse Image Search (RIS) and targeted query methodology.

**Step 1: Visual Context Extraction (Google Lens)**
To establish a baseline, I uploaded the provided image (`20260124_...`) to **Google Lens**. The visual search algorithm analyzed the background track barriers, vehicle liveries, and environmental lighting. This successfully identified the specific racing event and the year it took place based on the visual footprint of the cars.

**Step 2: Targeted Querying**
Once Google Lens identified the exact event, I focused on the challenge prompt's clues: "overslept and missed most of the race" and "whose in the lead." Knowing the exact race, I formulated targeted follow-up questions in Google Search (e.g., querying the race leaderboards, tandem cars, and nighttime race leaders for that specific event).

**Step 3: Correlating the Sequence**
The search results provided historical race coverage and leaderboard data. By cross-referencing the "twin" clue from the prompt with the race history, I uncovered the exact sequence of the two leading cars.

## 3. The Findings
By combining Google Lens for event identification with targeted search engine queries for historical race data, the sequence of the leading tandem pair was extracted:

* **Leading Car 1:** `21`
* **Leading Car 2:** `44`
* **Final Flag:** `texsaw{21_44}`

## 4. Conclusion
This challenge demonstrated the efficiency of modern OSINT tools. Rather than relying purely on manual visual inspection, leveraging visual search engines like Google Lens to establish a baseline context allows an investigator to quickly pivot to targeted text-based queries to uncover the exact data points required.
