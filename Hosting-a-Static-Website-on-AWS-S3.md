# 🚀 **Detailed Step-by-Step Guide: Hosting a Static Website on AWS S3**

## **Complete Implementation Guide with Screenshots Reference**

---

## **📌 Prerequisites**
- AWS Account with access to S3 service
- Basic understanding of JSON (for bucket policy)
- Static website files ready for upload

---
` 

## **🔰 STEP 1: Sign in to AWS Console**

1. Open your browser and navigate to [AWS Management Console](https://aws.amazon.com/console/)
2. Enter your credentials to sign in
3. **Region Selection:** Ensure "Asia Pacific (Mumbai)" is selected in the top-right corner
4. In the search bar, type "S3" and select **Amazon S3**


---

## **📦 STEP 2: Create an S3 Bucket**

### **2.1 Navigate to Buckets Section**
- From S3 dashboard, click on **"Buckets"** in the left sidebar
- Click the orange **"Create bucket"** button

### **2.2 Configure Bucket Settings**

| Setting | Value | Description |
|---------|-------|-------------|
| **Bucket name** | `aws-bucket-static-web-kishore` | Globally unique name |
| **AWS Region** | Asia Pacific (Mumbai) `ap-south-1` | Choose nearest to your audience |
| **Object Ownership** | ACLs disabled (recommended) | Keep default |
| **Block Public Access settings** | Uncheck "Block all public access" | **Required for static website** |
| **Bucket Versioning** | Disable | Optional for static sites |
| **Tags** | Optional | Add if needed |
| **Default encryption** | Disable | Can enable later if required |

### **2.3 Create the Bucket**
- Review all settings
- Click **"Create bucket"** at the bottom

> 📸 **Reference:** Screenshot 2026-03-13 115407.png shows the newly created bucket in the list with creation date March 13, 2026

---

## **📤 STEP 3: Upload Website Files**

### **3.1 Access Your Bucket**
- Click on your bucket name: `aws-bucket-static-web-kishore`
- You'll enter the bucket dashboard showing: Objects, Properties, Permissions, etc.

### **3.2 Prepare Your Files**
Your website should include:
- `index.html` (main page)
- CSS files
- JavaScript files
- Images and other assets
- Any additional HTML pages

### **3.3 Upload Files**

1. Click the **"Upload"** button
2. Either:
   - **Drag and drop** files into the upload area
   - Click **"Add files"** to browse and select
3. Select all 6 files from your local machine:
   - `TEMPLATE.txt`
   - `GOOGLE_SHEETS_SETUP.md`
   - `google-sheets-setup-guide.html`
   - `index.html`
   - `tooplate-event-invitation.css`
   - `tooplate-event-scripts.js`

4. **Upload Options:**
   - Destination: Keep as default (bucket root)
   - Storage class: **Standard**
   - Encryption: None (default)
   - Metadata: Optional

5. Click **"Upload"** button at the bottom

### **3.4 Verify Upload**
- After upload completes, click **"Close"**
- You should see all 6 files listed in the bucket
- Check columns: Name, Type, Last modified, Size, Storage class

> 📸 **Reference:** Screenshot 2026-03-13 115425.png shows all 6 files successfully uploaded with their details

---

## **🔐 STEP 4: Configure Bucket Policy for Public Access**

### **4.1 Navigate to Permissions**
- Click on your bucket name
- Click the **"Permissions"** tab

### **4.2 Check Block Public Access Settings**
- Look for **"Block public access (bucket settings)"**
- It should show: **"Block all public access: Off"**
- If it's ON, click **"Edit"** and uncheck all blocks

> 📸 **Reference:** Screenshot 2026-03-13 115510.png shows Block Public Access is OFF

### **4.3 Add Bucket Policy**

1. Scroll down to **"Bucket policy"** section
2. Click **"Edit"** or **"Create bucket policy"**

3. Copy and paste the following JSON:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::aws-bucket-static-web-kishore/*"
    }
  ]
}
```

### **4.4 Understanding the Policy**

| Element | Value | Purpose |
|---------|-------|---------|
| **Version** | 2012-10-17 | Policy language version |
| **Effect** | Allow | Grants permission |
| **Principal** | * | Anyone (public) |
| **Action** | s3:GetObject | Read-only access |
| **Resource** | arn:aws:s3:::bucket-name/* | All objects in bucket |

### **4.5 Save Policy**
- Click **"Save changes"**
- You should see a success message

> 📸 **Reference:** Screenshot 2026-03-13 115519.png shows the bucket policy JSON configuration

---

## **🌐 STEP 5: Enable Static Website Hosting**

### **5.1 Navigate to Properties**
- Click on your bucket name
- Click the **"Properties"** tab

### **5.2 Find Static Website Hosting Section**
- Scroll down to **"Static website hosting"**
- Currently it shows "Disabled"
- Click **"Edit"**

### **5.3 Configure Static Website Hosting**

1. **Enable:** Select **"Enable"**
2. **Hosting type:** Choose **"Host a static website"**
3. **Index document:** Enter `index.html`
4. **Error document:** Enter `error.html` (optional, create if needed)
5. **Redirection rules:** Leave blank (optional)

### **5.4 Save Configuration**
- Click **"Save changes"**
- You'll return to Properties tab
- Static website hosting now shows **"Enabled"**

### **5.5 Note Your Website Endpoint**
- In Properties tab, scroll to Static website hosting
- You'll see the endpoint URL:
```
http://aws-bucket-static-web-kishore.s3-website.ap-south-1.amazonaws.com
```
- **Copy this URL** - this is your live website address!

> 📸 **Reference:** Screenshot 2026-03-13 115538.png shows Static Website Hosting enabled with the endpoint URL

---

## **✅ STEP 6: Test Your Website**

### **6.1 Access via Endpoint**
- Open a new browser tab
- Paste your website endpoint URL
- Press Enter

### **6.2 Verify Content**
You should see your event invitation page with:
- "You're Invited" heading
- Event details:
  - **DATE:** December 31, 2025
  - **TIME:** 5:00 PM - 10:00 PM
- Proper styling from CSS
- Any interactive elements working

> 📸 **Reference:** Screenshot 2026-03-13 115647.png shows the successfully loaded webpage

---

## **📊 STEP 7: Verify Configuration (Optional)**

### **7.1 Check Account Snapshot**
- From S3 main dashboard
- View **"Account snapshot"** section
- Shows daily storage usage and activity

### **7.2 Monitor External Access**
- Check **"External access summary"**
- Monitors public access permissions
- Shows any findings from IAM Access Analyzer

> 📸 **Reference:** Screenshot 2026-03-13 115407.png shows these monitoring sections

---

## **🎯 Complete File Structure**
Your S3 bucket now contains:
```
aws-bucket-static-web-kishore/
├── index.html (main page - 9.3 KB)
├── TEMPLATE.txt (557 bytes)
├── GOOGLE_SHEETS_SETUP.md (4.0 KB)
├── google-sheets-setup-guide.html (14.7 KB)
├── tooplate-event-invitation.css (15.5 KB)
└── tooplate-event-scripts.js (3.8 KB)
```

---

## **⚡ Quick Commands (AWS CLI Alternative)**
If you prefer using AWS CLI instead of Console:

```bash
# Create bucket
aws s3 mb s3://aws-bucket-static-web-kishore --region ap-south-1

# Upload files
aws s3 cp . s3://aws-bucket-static-web-kishore/ --recursive

# Set bucket policy
aws s3api put-bucket-policy --bucket aws-bucket-static-web-kishore --policy file://policy.json

# Enable static website
aws s3 website s3://aws-bucket-static-web-kishore/ --index-document index.html
```

---

## **🔧 Troubleshooting Tips**

| Issue | Solution |
|-------|----------|
| **403 Forbidden** | Check bucket policy Principal is "*" |
| **404 Not Found** | Verify index.html exists in bucket root |
| **Files not loading** | Check all file names are correct (case-sensitive) |
| **CSS/JS not working** | Ensure paths in HTML are correct |
| **Website not accessible** | Verify Block Public Access is OFF |

---

## **📝 Important Notes**

1. **Bucket Name:** Must be globally unique across all AWS accounts
2. **Public Access:** Required for static hosting, but only for read-only
3. **Index Document:** Must be exactly `index.html` (case-sensitive)
4. **Region:** Choose based on your target audience for better latency

---

## **🚀 Next Level Enhancements**

1. **Custom Domain:** Connect your own domain using Route 53
2. **HTTPS:** Add CloudFront for SSL/TLS encryption
3. **CDN:** Use CloudFront for faster global delivery
4. **CI/CD:** Automate uploads with GitHub Actions
5. **Monitoring:** Enable S3 server access logs
6. **Cost Optimization:** Add lifecycle policies for old files

---

## **📸 Screenshot Reference Guide**

| Screenshot | Shows |
|------------|-------|
| 115407.png | S3 dashboard, bucket list, account snapshot |
| 115425.png | Uploaded files in the bucket |
| 115510.png | Permissions overview, Block Public Access settings |
| 115519.png | Bucket policy JSON configuration |
| 115538.png | Static website hosting enabled with endpoint |
| 115647.png | Live website - Event invitation page |

---

## **✅ Final Checklist**

- [x] S3 bucket created with unique name
- [x] Region set to Asia Pacific (Mumbai)
- [x] All 6 website files uploaded
- [x] Block Public Access turned OFF
- [x] Bucket policy configured for public read
- [x] Static website hosting ENABLED
- [x] Index document set to index.html
- [x] Website endpoint URL noted
- [x] Live website tested and working
- [x] Event invitation page displaying correctly

---

## **🎉 Congratulations!**
Your static website is now live on AWS S3 and accessible to anyone on the internet!

**Website URL:** 
```
http://aws-bucket-static-web-kishore.s3-website.ap-south-1.amazonaws.com
```

**Total Time Taken:** Approximately 15-20 minutes

**Cost:** Minimal (usually under $1/month for low traffic)

---


*This completes the detailed step-by-step implementation of hosting a static website on AWS S3.* 🚀

