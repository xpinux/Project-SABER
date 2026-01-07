# Microsoft Sentinel Detection Rules
Welcome to the **Detections** folder of this repository.  
Each detection rule is stored in its own folder, containing:
- A `.md` file with a detailed description, MITRE mapping, recommendations, and tuning guidance.
- A `.kql` file containing the KQL query.

## How to Use Detection Rules in Microsoft Sentinel
Follow these steps to deploy a detection rule:

### 1. Navigate to Analytics
1. Open your Microsoft Sentinel workspace.  
2. Go to **Configuration > Analytics**.  

### 2. Create a New Rule
1. Click **+ Create > Scheduled query rule**.  
2. Give the rule a **name** matching the detection folder
3. Copy the **description** from the `.md` file to the rule description.  
4. Add **MITRE ATT&CK mappings** if available.  

### 3. Set the Query
1. Copy the KQL query from the `.kql` file.  
2. Paste it into the **Set rule query** section.  

### 4. Define Entities
1. Map relevant fields such as `AccountName`, `Computer`, `TargetUserName` in the **Entity mapping** section.  
2. This ensures incidents are enriched with contextual information.  

### 5. Configure Scheduling
1. Set the **lookup period** (how far back the query searches).  
2. Set the **query frequency** (how often the query runs).  
3. Recommended values are usually listed in the detection `.md` file.  

### 6. Set Thresholds and Conditions
1. Apply thresholds or filters defined in the `.md` file (Most probably you won't have too, as it is set in the Query)
2. (Optional) Adjust thresholds to match your environment’s baseline activity.  

---
### 7. Simulate the Rule (CRUCIAL)
1. Use the **Simulate results** option before enabling the rule.  
2. This allows you to:
   - Verify the number of alerts generated.  
   - Fine-tune thresholds and timeranges.  
   - Identify potential false positives.
       
   <img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/b8006c5e-1c7a-4867-b08a-7b993b5b9084" />

### 8. Tune and Filter
- Exclude known **service accounts** or **maintenance hosts** to reduce false positives.  
- Consider grouping similar alerts if the query produces too many noisy results.  
- Re-run simulation until results are meaningful and actionable.  

### 9. Enable the Rule
- Once satisfied with tuning, enable the rule.  
- Monitor generated incidents and continue fine-tuning periodically.  

## Best Practices

- Always **simulate first** before enabling in production.  
- Customize thresholds and excluded hosts to reduce false positives.  
- Group or suppress noisy alerts to prevent alert fatigue.  
- Include **MITRE ATT&CK mappings** in the description to support threat modeling.  
- Periodically review active rules and tuning as your environment evolves.


