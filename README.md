# Bricktopia Construction Website – Cloud Server Project

**Student Name:** Ryan Idicula Thomas  
**Student Number:** 35874582  

**VM Name:** BricktopiaVM  
**Username:** ryan  
**Public IP:** 51.103.214.199  
**Domain:** https://bricktopiabybonztomz.com  
**Contact Email (for SSL):** ryanidiculathomas@gmail.com  

**Video Explainer:** https://drive.google.com/file/d/1pJR-a7VXIvRU2gYjr7I4LMRntGkXsYq1/view?usp=drive_link

---

## Project Overview:  

This project demonstrates the deployment of a construction business website for my dad using Azure Ubuntu VM, Apache web server, custom HTML/CSS/JS, custom domain, and HTTPS security.

### Website Contents:  

The website includes:  
- `index.html` (Home page)
- `about.html` (About Us page)
- `completed-projects.html`
- `ongoing-projects.html`
- 13 Individual project pages
- `contact.html` (Contact page)
- Images folder with logos and project photos

**Purpose:** This website provides a professional online presence for Bricktopia Construction and allows potential clients to view the projects.

**Outcome:** Website should be accessible from a custom domain with HTTPS enabled.

---

## Before Starting the project:  

Ensure you have:

- **Website files**: All `.html` files and an `images/` folder in a single folder (`BricktopiaWebsitehtml`)  
**Local Website Files:**
  <img width="1718" height="1480" alt="BricktopiaHTML-Folder" src="https://github.com/user-attachments/assets/eb3d85e5-b908-4670-90de-079d8c604194" />
 
**Images Files:**
<img width="1718" height="1202" alt="ImagesInDetail" src="https://github.com/user-attachments/assets/b1ddded1-5fd8-416d-840d-6f44e69d7682" />  

*BricktopiaWebsitehtml folder containing all HTML files and images directory*
  
- **Azure account** to create VM
- **Namecheap account** to buy a domain
- **Software installed locally**:
  - PowerShell (Windows)
  - WinSCP (for file transfer)
  - Browser for testing
- **Domain purchased**

### Screenshot References:  

**Domain Purchase Page:**  
<img width="1812" height="390" alt="BuyDomain" src="https://github.com/user-attachments/assets/2000b6d4-6c96-4446-9c6f-b82565dd098e" />  
*Screenshot showing domain ready to purchase on Namecheap*

**Domain Purchase Confirmation:**
<img width="1156" height="1050" alt="DomainBought" src="https://github.com/user-attachments/assets/fe1c1dfa-1632-45d6-9fee-9b0905c762f6" />  
*Receipt showing domain purchased - With Promocode it became cheaper.*  

---  

## Phase 1 – Azure VM Setup:  

### Steps

1. Log into Azure portal
2. Create a **new Ubuntu VM**:
   - VM Name: `BricktopiaVM`
   - OS: Ubuntu 22.04 LTS
   - Size: B1s (for cost saving)
3. Configure **Network Security Group (NSG)** to allow:
   - SSH (port 22)
   - HTTP (port 80)
   - HTTPS (port 443)

### Screenshot References:  

**Azure VM Overview:**  
<img width="2880" height="1346" alt="VM-OverviewPage" src="https://github.com/user-attachments/assets/cfa25fa5-4b53-479c-a89d-0d13b0e5c26c" />  
*Azure portal showing BricktopiaVM overview with running status and configuration details*  

**Creation of Port Rules in NSG**  

<img width="2879" height="1432" alt="image" src="https://github.com/user-attachments/assets/6b751d9c-da8d-44d6-bfa0-c6daf6b5e64e" />  

**SSH Connection Established:**
<img width="2328" height="1206" alt="SSH-SessionPowerShell" src="https://github.com/user-attachments/assets/8e4ea35f-4c0b-47d2-9977-eacdabab2507" />  
*PowerShell terminal showing successful SSH connection to Ubuntu VM*

---  


## Phase 2 – Connect to VM and Update System:

### Connect via SSH (PowerShell on Windows)  

ssh ryan@51.103.214.199  

Once entered, you will see that you're inside the Ubuntu VM in PowerShell:  

ryan@BricktopiaVM:~$  

  
### Update System  

sudo apt update
sudo apt upgrade -y  

**System Update Completed:**
<img width="2308" height="1218" alt="SudoAPTUpdateAndUpgrade" src="https://github.com/user-attachments/assets/077347e2-f5c9-486e-a477-aafa385fa96c" />  
I have done it before so I have nothing left to upgrade, install, remove.  

*Terminal output shows successful apt update and upgrade completion, ensuring system is up-to-date and ready for Apache installation*  

---

## Install Apache:  

### Installation Commands  
  
sudo apt install apache2 -y  
sudo systemctl enable apache2  
sudo systemctl start apache2  

### Verify Apache is Running  
  
sudo systemctl status apache2   

Then test if the website works with public IP in the web browser.

### Screenshot References: 

**Default Apache Page:**  
<img width="915" height="632" alt="DefaultApache" src="https://github.com/user-attachments/assets/333eaa98-1519-4b1f-982c-e7cc28d36cba" />  

*Default Apache2 Ubuntu page confirming successful installation and web server is running*

### Troubleshooting:  

If page doesn't load, ensure NSG allows HTTP port 80.

If firewall (UFW) is active:  

sudo ufw allow 'Apache Full'  
sudo ufw reload  

---

## Now Upload Website Files to VM:  

### Using WinSCP  

1. Open WinSCP (download from the website if needed)
2. Fill in the connection details:
   - **Host:** 51.103.214.199
   - **Port:** 22
   - **Username:** ryan
   - **Protocol:** SCP
3. Navigate to the Ubuntu directory
4. Set **Remote directory:** `/tmp/`
5. Drag `BricktopiaWebsitehtml` folder to `/tmp/`

### Verify Upload in SSH  

ls -l /tmp
ls -l /tmp/BricktopiaWebsitehtml  


### Screenshot References: 

**WinSCP File Transfer Interface:**  
  
<img width="2136" height="1264" alt="WinSCP" src="https://github.com/user-attachments/assets/28b05646-ddfd-4f8c-a673-d57234a082d5" />  
*WinSCP interface showing BricktopiaWebsitehtml folder being uploaded to /tmp/ directory*

**File Located in temp folder**   

<img width="2332" height="1204" alt="FileFoundTempFolder" src="https://github.com/user-attachments/assets/efcbb59e-741f-47ff-9552-adea3d9df85a" />  

*BricktopiaWebsitehtml folder is located in /tmp/ directory*
---

## Move Files to Apache Root:  

Once done, follow these commands to transfer the files safely:

sudo rm -rf /var/www/html/*  
sudo mv /tmp/BricktopiaWebsitehtml/* /var/www/html/  
sudo chown -R www-data:www-data /var/www/html/  
sudo chmod -R 755 /var/www/html/  
sudo systemctl restart apache2  

### Verify Files Are in Place:  

ls /var/www/html/  

**Files Successfully Transferred:**  

<img width="2168" height="1204" alt="FilesTransferredProof" src="https://github.com/user-attachments/assets/0d5ef4ff-670f-4bf1-8831-292c15986609" />  

*Terminal output confirming all website files successfully uploaded to to Apache Root*  

Test website in browser: `http://51.103.214.199` – It will show the actual website

**Website Accessible via Public IP:**  
<img width="2880" height="1520" alt="WebsiteWithPublicIPOnly" src="https://github.com/user-attachments/assets/b8299e9f-5d8e-4596-af59-c9f58128be4c" />  

*Bricktopia website successfully loaded using VM's public IP address*

### Screenshot References:  

**Home Page HTML Code:**  
<img width="2880" height="1514" alt="IndexHTML" src="https://github.com/user-attachments/assets/3dbcb34b-9d98-4f81-bf89-e889e55004db" />  

*Bricktopia Construction home page (index.html) code shown.*

**About Us Page:**    

<img width="2880" height="1518" alt="AboutUs" src="https://github.com/user-attachments/assets/d08ed369-71d1-40be-ac10-068f8de711e7" />  

*About Us page (about.html) displaying company information*

**Contact Page:**  

<img width="2880" height="1522" alt="ContactUs" src="https://github.com/user-attachments/assets/cc08e69d-e8da-422b-aef5-450c7c58d36f" />  

*Contact page (contact.html) with client inquiry form*

---

## Phase 3 – Domain Setup (Namecheap) :

### Configure DNS Records

1. Log into Namecheap
2. Add A records for your domain:

| Host | Value | TTL |
|------|-------|-----|
| @ | 51.103.214.199 | Automatic |
| www | 51.103.214.199 | Automatic |

3. Wait for DNS propagation (usually minutes but it can take upto 1 hour)

### Screenshot References: 

**Namecheap Domain Dashboard:**  
<img width="2880" height="1360" alt="NameCheapDashboard" src="https://github.com/user-attachments/assets/d9f23284-928b-4340-9daa-78f8e5658466" />  

*Namecheap dashboard showing domain management interface*  

**DNS Configuration:**  
<img width="2702" height="1440" alt="DNSSetup" src="https://github.com/user-attachments/assets/84d33455-1479-4f1c-bca5-cbef3385a8a5" />  

*Advanced DNS page showing A records configured to point to VM's public IP*  

**Website Accessible via Domain:**  
<img width="2880" height="1522" alt="DomainAndHTTPSAndSSL" src="https://github.com/user-attachments/assets/f99ae0b3-6ca0-4af0-94f5-9e38c7b6648b" />  

*Bricktopia website successfully accessible through custom domain name*

---  

## Phase 4 – Enable HTTPS with Certbot (Let's Encrypt) :

### Install Certbot and Apache Plugin  

sudo apt install certbot python3-certbot-apache -y  

### Run Certbot  

bash  
sudo certbot --apache  

### Follow Certbot Prompts  

During the setup wizard:  

1. **Enter email:** `ryanidiculathomas@gmail.com`  
2. **Agree to terms**  
3. **Select your domain**  
4. **Redirect HTTP → HTTPS** (recommended)  

### Test HTTPS  

Visit in browser: `https://bricktopiabybonztomz.com`  

It should display the lock icon showing a secure connection.

### Screenshot References:  

**HTTPS Certificate Valid:**  
<img width="2880" height="1520" alt="LockCertificateValid" src="https://github.com/user-attachments/assets/4c95b955-1dc1-46d5-b06d-cec22602b71b" />  

*Browser address bar showing padlock icon and valid SSL certificate from Let's Encrypt*

### Verify Auto-Renewal  

sudo systemctl status certbot.timer  

---  

## Final Verification & Testing :

### Verify Apache  

sudo systemctl status apache2  

### Verify Files in Web Root  

ls -l /var/www/html/  

### Browser Checks  

Test all access methods:  
- `http://51.103.214.199`   
- `https://bricktopiabybonztomz.com`  
- `www.bricktopiabybonztomz.com`

### Screenshot References:  

**Website Test Page 1:**
<img width="2876" height="1522" alt="TestSite1" src="https://github.com/user-attachments/assets/0725877a-9b4e-4b9e-becc-404bec146b5f" />  

*Testing one of the website pages to verify all content loads correctly*

**Website Test Page 2:**  
<img width="2880" height="1522" alt="TestSite2" src="https://github.com/user-attachments/assets/620d2c23-0f42-4aba-b412-48404e7fdadb" />  

*Testing another page to ensure navigation and links work properly across the site*

**URL Website Test 1:**  
<img width="2880" height="1438" alt="image" src="https://github.com/user-attachments/assets/b842e791-73cb-44b3-b9c3-be8c986dc379" />  

*Testing http://51.103.214.199 works.*  

**URL Website Test 2:**  
<img width="2880" height="1430" alt="image" src="https://github.com/user-attachments/assets/40f4855d-b8a0-4578-ace7-10ad1874633d" />  

*Testing https://bricktopiabybonztomz.com works.*  

**URL Website Test 3:**  
<img width="2879" height="1434" alt="image" src="https://github.com/user-attachments/assets/ba240276-67b8-4de9-a0af-6988484102f2" />  

*Testing www.bricktopiabybonztomz.com works.* 
---

**Project Completed.**
