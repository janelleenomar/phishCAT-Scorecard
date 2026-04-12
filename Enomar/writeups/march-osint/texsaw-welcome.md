# 📝 Challenge Write-up: WELCOME!

| Attribute | Details |
| :--- | :--- |
| **Event** | TexSAW 2026 |
| **Category** | Misc / Sanity Check |
| **Difficulty** | Easy |
| **Target** | `irc.texsaw.org` |

## 1. The Challenge Scenario
This is the standard "sanity check" challenge designed to ensure players can successfully connect to the competition's communication infrastructure. The challenge instructions simply stated: *"Check out our IRC server and run the command /motd! irc.texsaw.org"*

## 2. The Step-by-Step Solution
To solve this, I needed to use an Internet Relay Chat (IRC) client to connect to the provided server address and read the server's welcome message.

**Step 1: Connecting to the IRC Server**
Using my Linux environment, I launched the `irssi` command-line IRC client. I connected to the server by pointing the client to `irc.texsaw.org`.

**Step 2: Retrieving the MOTD**
Upon successfully connecting to the server, the Message of the Day (MOTD) automatically populated in the terminal. The server administrators had embedded the flag directly inside the announcement block alongside warnings about brute-forcing.

## 3. The Findings
By connecting to the IRC infrastructure and reading the MOTD, the welcome flag was retrieved:

* **Flag:** `texsaw{w31c0M3_t0_t3xSAW_2026!}`

## 4. Conclusion
This challenge tested basic familiarity with legacy communication protocols (IRC) and terminal-based clients like Irssi, acting as a gateway to the rest of the competition infrastructure.
