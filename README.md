# Bricktopia Construction Website – Cloud Server Project

**Student Name:** Ryan Idicula Thomas  
**Student Number:** 35874582  

**VM Name:** BricktopiaVM  
**Username:** ryan  
**Public IP:** 51.103.214.199  
**Domain:** https://bricktopiabybonztomz.com  
**Contact Email (for SSL):** ryanidiculathomas@gmail.com  

**Video Explainer:** [BricktopiaVideoExplainer.mp4]

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
