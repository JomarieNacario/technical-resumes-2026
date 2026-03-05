# 🚀 Tech-Forward Solutions Architect & AI Strategist
### U.S. Army Veteran | AWS Solutions Architect | AI Automation Expert

Welcome to my professional repository. I specialize in the intersection of **Cloud Infrastructure**, **Generative AI Automation**, and **Strategic Sales**. My background combines the methodical discipline of military marine engineering with high-performance sales experience at Apple and entrepreneurial leadership.

---

## 📄 Targeted Resumes
- [🚀 Modern Innovation](./Modern_Innovation_Resume.md) - AI Strategy & Technical Sales
- [🤖 AI Specialist](./AI_Automation_Specialist.md) - Generative AI & Automation
- [☁️ Cloud Architect](./Cloud_Solutions_Architect.md) - AWS/Azure Infrastructure
- [🛠️ Enterprise IT](./Enterprise_IT_Support.md) - Senior Systems Support

---

## 📬 Connect With Me
- **LinkedIn:** [LinkedIn](www.linkedin.com/in/j-nacario)
- **Portfolio:** [Github](https://github.com/JomarieEliason)
- **Email:** jomarienacario15@gmail.com

*Last Updated: March 2026*
""",
    "Modern_Innovation_Resume.md": """# JOMARIE ELIASON
**Strategic Technical Sales & IT Support Professional**

### PROFESSIONAL SUMMARY
Dynamic Tech-Forward Professional and U.S. Army Veteran specializing in AI Automation, Cloud Architecture, and Revenue Generation. Expert in the RIGS framework for prompt engineering and "vibe coding" custom AI-powered applications. 

### CORE COMPETENCIES
- **AI Fluency:** Prompt Engineering (RIGS), Vibe Coding, Data Intelligence.
- **Strategic Sales:** B2B Account Management, Consultative Selling at Apple and Aurakore.
- **Leadership:** U.S. Army Veteran with elite troubleshooting discipline.

### CERTIFICATIONS
- Google AI Professional Certificate (2026)
- AWS Cloud Support Associate (2025)
""",
    "AI_Automation_Specialist.md": """# JOMARIE ELIASON
**AI & Automation Specialist**

### EXPERTISE
AI-Native Technical Lead specialized in deploying Generative AI frameworks to solve operational challenges. Expert in building custom AI-powered applications without code ("Vibe Coding") to solve operational bottlenecks.

### AI COMPETENCIES
- **Prompt Engineering:** Expert in RIGS framework.
- **Data Intelligence:** Visualizing unstructured data via Gemini and BigQuery.
- **Automation:** Deploying AI agents for sales and support workflows.

### CERTIFICATIONS
- Google AI Professional Certificate (2026)
- MTA: Software Development Fundamentals
""",
    "Cloud_Solutions_Architect.md": """# JOMARIE ELIASON
**Cloud Solutions & Support Architect**

### PROFESSIONAL SUMMARY
**AWS Certified Solutions Architect & U.S. Army Veteran** with a deep focus on cloud migration, infrastructure reliability, and multi-cloud environments (AWS/Azure). Recently credentialed as an **AWS Cloud Support Associate (2025)**, combining advanced troubleshooting skills with a strategic understanding of scalable architecture.

### CLOUD & TECHNICAL COMPETENCIES
* **Architecture:** VPC configuration, High Availability (Multi-AZ), IAM Security, Route53.
* **Storage & Compute:** EC2, S3, RDS, Lambda, and CloudWatch monitoring.
* **Support:** Enterprise hardware/software resolution, virtualization, and Linux administration.
* **Automation:** Integrating AI-driven monitoring and automated recovery scripts.

### EXPERIENCE HIGHLIGHTS
**AURAKORE IT SOLUTIONS** | Technical Account Executive
* Prototyped and proposed optimized AWS/Azure architectures.
**U.S. ARMY** | Marine Engineering Specialist
* Diagnosed and repaired critical engineering systems under high-stakes conditions.

### CERTIFICATIONS
* **AWS Cloud Support Associate** | 2025
* **AWS Certified Solutions Architect – Associate** | 2022
* **Microsoft Certified: Azure Fundamentals (AZ-900)** | 2021
""",
    "Enterprise_IT_Support.md": """# JOMARIE ELIASON
**Senior IT Support Specialist**

### PROFESSIONAL SUMMARY
Senior IT Support Specialist and U.S. Army Veteran with 8+ years experience in hardware/software resolution and network security. Expert in enterprise systems administration and integrating AI automation into traditional helpdesk workflows.

### TECHNICAL SKILLS
- **Systems:** Active Directory, Office 365, Windows/Linux Server.
- **Troubleshooting:** High-pressure hardware resolution (Apple/Military).
- **Networking:** Security foundations and virtualization.

### CERTIFICATIONS
- Google IT Support Professional Certificate (2025)
- Google AI Professional Certificate (2026)
"""
}

def upload_to_github(filename, content):
    url = f"https://api.github.com/repos/{GITHUB_REPO}/contents/{filename}"
    headers = {
        "Authorization": f"token {GITHUB_TOKEN}",
        "Accept": "application/vnd.github.v3+json"
    }
    
    # Check if file exists to get SHA
    response = requests.get(url, headers=headers)
    sha = None
    if response.status_code == 200:
        sha = response.json().get('sha')
    elif response.status_code == 401:
        print(f"Error: 401 Unauthorized. Your token for {GITHUB_REPO} is invalid.")
        return

    data = {
        "message": f"Full Portfolio Content Sync: {filename}",
        "content": base64.b64encode(content.encode('utf-8')).decode('utf-8')
    }
    
    if sha:
        data["sha"] = sha
        
    res = requests.put(url, headers=headers, data=json.dumps(data))
    if res.status_code in [200, 201]:
        print(f"Successfully uploaded: {filename}")
    else:
        print(f"Error uploading {filename}: {res.text}")

def main():
    if GITHUB_TOKEN == "YOUR_GITHUB_TOKEN_HERE" or GITHUB_TOKEN == "":
        print("Please update the GITHUB_TOKEN in the script.")
        return
    
    print(f"Connecting to {GITHUB_REPO}...")
    # Add index.html to the upload list
    # Note: Ensure index.html is in your local directory or hardcode it here
    for name, text in resumes.items():
        upload_to_github(name, text)

if __name__ == "__main__":
    main()
