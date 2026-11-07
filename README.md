# Wireshark SOC Training Labs - Completion Report

**Author:** TheFlow
**Date:** November 2026
**Status:** 100% Completed

## Overview

This repository contains my notes and proof of completion for a series of Security Operations Center (SOC) labs focused on network traffic analysis using Wireshark. The modules covered essential incident response techniques, including tracking TCP streams, extracting plaintext credentials, identifying brute-force attacks, and analyzing VoIP traffic.

## 🔬 Core Skills & Concepts Mastered

During these labs, I gained hands-on experience utilizing Wireshark display filters and built-in statistics to investigate network anomalies.

### 1. TCP Connection & Port Analysis

* **Isolating SYN Packets (Connection Requests):** `tcp.flags.syn == 1`

* **Finding Open Ports (SYN-ACK):** `tcp.flags.syn == 1 and tcp.flags.ack == 1`

* **Finding Closed Ports (RST-ACK):** `tcp.flags.reset == 1 and tcp.flags.ack == 1`

* **Distinguishing Attacks:** Differentiated between Stealth SYN Scans (reconnaissance across multiple ports) and SYN Floods (Denial of Service targeting a single port).

### 2. Investigating Specific Activity

* **Targeted Port Analysis:** Identified suspicious repetitive traffic hitting port 52311, which is the default port used by the BigFix Enterprise Suite (BES) for agent-server communications.

  * *Filter used to count destination ports:* `tcp.flags.syn == 1 and tcp.flags.ack == 0 and tcp.srcport == 52311`

* **HTTP Credential Extraction:** Tracked POST requests over legacy HTTP to extract plaintext usernames and passwords from URL-encoded HTML forms.

* **FTP Brute Force Detection:** Used `Statistics > Protocol Hierarchy` to identify high volumes of FTP traffic. Applied the filter `ftp.response.code == 530` ("Not logged in") to track failed authentication attempts indicative of a brute-force attack.

* **VoIP Analysis:** Used Wireshark's Telephony tools to track SIP signaling and extract/playback RTP media streams to identify active voice codecs (like G.711 PCMU/PCMA) and listen to intercepted calls.

## 🏆 Lab Results & Proof of Completion

Below is the documented proof of successfully completing the Wireshark SOC Lab modules with outstanding (100%) marks.

### Lab 4: Follow TCP Stream

Successfully tracked and reconstructed raw application data across a client-server conversation.
**Result:** Identified a Stealth SYN scan (Port Scan) based on network behavior.

### Lab 5: Follow TCP Stream, part 2

Located hidden data/notes inside extracted HTTP web page payloads traversing the network.

### Lab 6: HTTP Plain Text Credentials

Intercepted legacy web traffic to identify compromised user accounts and plaintext passwords.

### Lab 7: Brute Force Catch

Analyzed application-layer errors to identify the protocol, attacker, and success/failure vectors of a brute-force attack.
**Result:** Identified an attacker using the FTP protocol, trying different passwords on the same username.

### Lab 8: VoIP Call Replay

Analyzed VoIP call setups (SIP) and utilized the RTP player to decode and listen to unencrypted network voice traffic.
**Result:** Recommended using SRTP for secure Voice over IP calls to encrypt payloads.
