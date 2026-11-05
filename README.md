# INSY7315 - TEAM LOGIX

 Group members:
- ST10439133 - Camryn Naidoo
- ST10441399 - Suvan Samlall
- ST10451026 - Calib Frank
- ST10446908 - Caleb Ragaven
- ST10296234 - Joshua Chetty
- ST10451537 - Keshvir Parthab

Website Hosting Demo YouTube Link: https://youtu.be/Uxa4gDWenjY

Website Walkthrough Demo YouTube Link: https://youtu.be/403yAoKpoDI?si=AOJNTbFSH48ZFpVm

Website API Link: https://github.com/ST10441359/AdvancedAirAPI.git

Website GitHub Link:https://github.com/ST10441359/HvacWebsite.git

---

# Advanced Aircon Website — Public Customer Gateway & Catalogue

A comprehensive React and ASP.NET Core website for HVAC customer acquisition, product browsing, and intelligent sizing. Built to work seamlessly alongside the Advanced Aircon Android App, sharing the same Supabase backend without interfering with its operations.

## About

The Advanced Aircon Website serves as the public-facing digital front door for Advanced Air Conditioning. It streamlines the customer journey from discovering the brand and calculating room requirements to requesting a detailed quote or booking an emergency callout all without requiring a login or app download. 

It is designed to complement the internal Android App: where the app handles authenticated field operations (manager dashboards, technician tracking), the website handles public lead generation and customer self-service.

## The Problem It Solves

HVAC businesses struggle with:
- Slow enquiry processes reliant on phone calls and static business cards
- Customers being unable to self-serve their own BTU sizing requirements
- High drop-off rates due to a lack of digital product catalogues
- Frustrating experiences where customers must phone in just to get a baseline quote

The Advanced Aircon Website solves this with a 24/7 responsive digital showroom, an interactive BTU calculator, and frictionless lead capture forms that format data directly into the business's inbox.

## Key Features

### Public Digital Front Door
- No login or registration required for customers.
- Fully responsive design (mobile, tablet, desktop) built with Tailwind CSS.
- Modern React (Vite) single-page application architecture.

### Home Page & Brand Trust
- Hero section with three primary CTAs: Get a Quote, Book a Callout, BTU Calculator.
- Stats bar proving credibility (500+ jobs, 15+ years, 24/7 service, 100%).
- Six core service categories fetched dynamically from the API.
- "Why Choose Us" trust section featuring F-Gas certification, fixed pricing, and 12-month guarantees.
- Emergency "AC Broken Down?" banner with a direct clickable phone number.

### Live Product Catalogue
- Full product grid fetched directly from Supabase.
- Cards display: Name, Model, Price (ZAR), BTU rating, coverage area, and four key features.
- Dynamic image loading from Supabase Storage.
- Simplified customer-facing UX (the Android app retains advanced filtering for technicians).

### Intelligent BTU Calculator
- Simplified 3-field form: Room Size (m²), Number of Occupants, Room Type.
- Instantly calculates recommended BTU range and displays matching products from the database.
- Designed for customers at home who do not know technical HVAC sizing specifications.

### Customer Enquiry & Lead Capture
- **Book a Callout:** Fast-track emergency form capturing urgency, address, and issue description. Includes a prominent "Call Now" fallback on the success screen.
- **Request a Quote:** Comprehensive multi-room form. Users can add/remove unlimited rooms, set urgency levels, and choose service types.
- **Direct Email Integration:** Both forms use the direct email intergration to format all inputted data into a clean, structured email and open the user's default email client instantly.
- **Frontend Validation:** The submit button remains strictly disabled until the user ticks the privacy consent checkbox.

## Architecture

The website follows a strict **Decoupled Read-Only Architecture**. 
The React frontend handles UI and state. It makes HTTP `GET` requests to the ASP.NET Core Web API. The API queries Supabase (PostgreSQL). Crucially, the website is designed so that it only *reads* data. It never uses `POST`, `PUT`, or `DELETE` requests, guaranteeing zero interference with the Android app's database.

## Tech Stack

| Layer | Technology |
|-------|-----------|
| **Frontend** | React (Vite), TypeScript, Tailwind CSS |
| **Routing** | React Router DOM |
| **HTTP Client** | Axios |
| **Icons** | Lucide React |
| **Backend** | ASP.NET Core Web API (.NET 8) |
| **ORM** | Entity Framework Core (Npgsql) |
| **Database** | Supabase (PostgreSQL) |
| **Caching** | ASP.NET Core `IMemoryCache` |
| **Forms** | React State + HTML5 Validation + `mailto:` Protocol |
| **Frontend Hosting** | Cloudflare Pages |
| **Backend Hosting** | Render (Docker Web Service) |

## Getting Started

### Prerequisites
- Node.js (v18 or newer)
- .NET 8 SDK
- Supabase project with a `products` and `services` table (and a public storage bucket named `products`)

### Configure the Backend (ASP.NET API) locally
1. Open the AdvancedAirAPI project.
2. In appsettings.json (or user secrets), configure your Supabase connection string
3. Run the API:
   dotnet run
   API will run on https://127.0.0.1:8080

### Configure the Frontend (React) locally 
1. Open the HvacWebsite project.
2. Create a .env.local file in the root:
   VITE_API_BASE_URL=https://127.0.0.1:8080
3. Install dependencies and start the Vite server:
   npm install
   npm run dev
   Frontend will run on https://localhost:5173

## Hosted On Cloudflare & Render
<img width="892" height="580" alt="image" src="https://github.com/user-attachments/assets/57b00179-0324-4a04-ba66-c6b1caebf6b9" />

Render – AdvancedAirAPI Production Deployment Render dashboard showing the successful deployment of the AdvancedAirAPI Docker web service, with the production instance marked as Live

<img width="912" height="581" alt="image" src="https://github.com/user-attachments/assets/7fc856d0-2c45-4674-b305-b66be3dde38d" />

Cloudflare – AdvancedAir Frontend Production Deployment Cloudflare Workers & Pages dashboard displaying the deployment history of the AdvancedAir frontend, with the latest production deployment marked as Ready.

## Security Notes

- **Read-Only API:** The ASP.NET API is configured to only accept `GET` requests to prevent any write-access to the shared database.
- **Mailto Protocol:** No sensitive customer data (names, addresses, phone numbers) is stored in the database. It is formatted locally in the browser and handed off to the user's email client, ensuring POPIA compliance.
- **CORS Configuration:** The backend is strictly configured to only accept traffic from the authorized frontend domains.

## AI Usage

1. Accelerating Responsive UI Layouts (Tailwind CSS)
We used AI to rapidly generate and troubleshoot Tailwind CSS utility classes. Instead of spending hours writing custom CSS for media queries, we used AI to help us structure the mobile-first grid layouts. For example, when ensuring the product cards scaled perfectly from a 1-column mobile view to a 3-column desktop view, AI helped us identify the correct responsive breakpoint prefixes (md: grid-cols-2 lg: grid-cols-3), which drastically sped up our styling process.
AI Used: https://chatgpt.com/c/6aeb8388-b7ac-83ea-936c-015a330bf4

2. Debugging Complex Form State & Validation
AI was incredibly useful for debugging React state logic, specifically on the multi-room 'Request a Quote' page. When we needed to implement the strict validation logic—where the submit button stays physically greyed out and disabled until the user ticks the consent checkbox—we used AI to help us write the dynamic template literal logic for the button's className and the disabled attribute. It helped us catch edge cases we might have missed, like preventing users from submitting the form using the 'Enter' key.
AI Used: https://chatgpt.com/c/6aeb8388-b7ac-83ea-936c-015a330bf4

3. Formatting the mailto: Protocol Payload
Formatting form data into a valid mailto: URL was tricky because of the strict syntax required for email bodies. We used AI to assist in writing the encodeURIComponent JavaScript logic that loops through the multi-room array, strips out empty fields, and formats the entire form state into a clean, line-broken text string. This ensured that when the customer's email app opened, the data looked professional and was readable, rather than a messy block of text.
AI Used: https://chatgpt.com/c/6aeb8388-b7ac-83ea-936c-015a330bf4

## Workflow Diagram
<img width="1793" height="664" alt="image" src="https://github.com/user-attachments/assets/9d22bf50-2e0c-4377-8b21-9af14bf16f91" />

## References
React. 2026. React Documentation. [Online]. Available at: https://react.dev/ [Accessed: 3 November 2026].

Vite. 2026. Vite Documentation. [Online]. Available at: https://vitejs.dev/ [Accessed: 3 November 2026].

Tailwind Labs. 2026. Tailwind CSS Documentation. [Online]. Available at: https://tailwindcss.com/ [Accessed: 2 November 2026].

Microsoft. 2026. ASP.NET Core Web API Documentation. [Online]. Available at: https://learn.microsoft.com/en-us/aspnet/core/web-api/ [Accessed: 2 November 2026].

Microsoft. 2026. Entity Framework Core. [Online]. Available at: https://learn.microsoft.com/en-us/ef/core/ [Accessed: 2 November 2026].

Supabase. 2026. Supabase Documentation. [Online]. Available at: https://supabase.com/docs [Accessed: 3 November 2026].

Render. 2026. Deploy for Free. [Online]. Available at: https://render.com/docs/free [Accessed: 2 November 2026].

Cloudflare. 2026. Cloudflare Pages Documentation. [Online]. Available at: https://developers.cloudflare.com/pages/ [Accessed: 2 November 2026].

IEEE Xplore. 2025. Design and Implementation of an Intelligent Facility Management Dashboard for Commercial Buildings. [Online]. Available at: https://ieeexplore.ieee.org/document/11038388 [Accessed: 1 November 2026].

IEEE Xplore. 2024. A Cloud-Based Platform for HVAC Maintenance Management and Quote Approval Workflows. [Online]. Available at: https://ieeexplore.ieee.org/document/10444775 [Accessed: 1 November 2026].
