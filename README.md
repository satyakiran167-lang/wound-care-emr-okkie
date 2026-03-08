# Wound Care EMR

Wound Care EMR is a simple web-based Electronic Medical Record (EMR) system designed for wound care management.  
This application allows healthcare providers to record patient data and manage basic patient information through a lightweight web interface connected to Google Sheets as the database.

## Author
Ns. Oki Hartono, S.Tr.Kep., CCWC

## Features
- Patient registration
- Automatic Medical Record Number (MRN) generation
- Patient database table
- Real-time data synchronization with Google Sheets
- Dashboard showing total patient count
- Simple and lightweight interface
- Web-based system accessible via browser

## Technologies Used
- HTML
- CSS
- JavaScript
- Google Apps Script
- Google Sheets (Database)
- GitHub Pages (Hosting)

## System Architecture

Web Application (HTML + JavaScript)  
↓  
Google Apps Script API  
↓  
Google Sheets Database

## Database Structure

The Google Sheets database contains the following columns:

| MRN | Name | Date_of_Birth | Gender | Address | Phone |
|-----|------|---------------|--------|---------|-------|

## How to Use

1. Open the web application.
2. Navigate to the **Patients** menu.
3. Fill in the patient information form.
4. Click **Save Patient**.
5. The patient data will automatically be saved to the database and displayed in the patient table.

## Deployment

The application is deployed using **GitHub Pages** and connected to **Google Apps Script Web API** for database interaction.

## Future Development

Planned improvements include:

- Wound assessment records
- Patient treatment timeline
- Image upload for wound documentation
- Advanced patient search and filtering
- User authentication system

## License
This project is intended for educational and research purposes.
