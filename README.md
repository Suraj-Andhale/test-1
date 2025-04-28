#!/bin/bash

echo "=== Oracle RAC Cluster Configuration ==="

echo -e "\n--- Cluster Nodes ---"
olsnodes

echo -e "\n--- CRS Status ---"
crsctl status resource -t

echo -e "\n--- CRS Configuration ---"
crsctl config crs

echo -e "\n--- Running Oracle Instances ---"
ps -ef | grep pmon | grep -v grep

echo -e "\n--- Interconnect Interfaces ---"
oifcfg getif

echo -e "\n--- SCAN Configuration ---"
srvctl config scan

echo -e "\n--- SCAN Listeners ---"
srvctl config scan_listener

# Ask for DB name and get its status
read -p $'\nEnter the DB unique name (e.g., orcl): ' DB_NAME

echo -e "\n--- Database Status for $DB_NAME ---"
srvctl status database -d "$DB_NAME"

echo -e "\n--- Database Configuration for $DB_NAME ---"
srvctl config database -d "$DB_NAME"
