# Chat2Geo: A ChatGPT-Like Web App for Remote-Sensing-Based Geospatial Analysis

Chat2Geo is a Next.js 15 application providing a chatbot-like user interface for performing remote-sensing-based geospatial analyses. It leverages Google Earth Engine (GEE) in the backend to process and analyze various remote sensing datasets in real time. Users can upload their own vector data, run advanced geospatial queries, and integrate the results with an AI Assistant for specialized tasks such as **land cover mapping**, **change detection**, and **air pollutant monitoring**. 

Chat2Geo also has advanced knowledge retrieval based on Retrieval-augmented generation (RAG), which can integrate geospatial analysis with non-geospatial/textual information. 

The app also has authentication and database integrations, making it almost a complete package. 

Chat2Geo inherits a large portion of its building blocks from the GRAI 2.0 app that is under development at GeoRetina (www.georetina.com). In parallel with GRAI 2.0 (which I plan to open-source once it's stable), I will also keep Chat2Geo updated for the community.


https://github.com/user-attachments/assets/d9940a0e-10c8-4d0e-9ec9-3dfd0966c664



## Contributing 🛠️

 - If you're interested in contributing to this project, please contact me at `shahabj.github@gmail.com`.
 - If you are a new contributor, please first check out our [Contributing Guidelines](./CONTRIBUTING.md) to get started.


## Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
- [Current Analyses](#current-analyses)
- [Considerations](#considerations)

---

## Features ✨

1. **Chat-Style Interface**

   - Interact with the system using natural language.
   - The AI Assistant can execute various **geospatial functions** on your behalf.

2. **Google Earth Engine Integration**

   - Real-time access to satellite imagery and remote sensing datasets.
   - Seamless backend processing for large-scale geospatial computations.

3. **Import Your Own Vector Data**

   - Upload and manage personal vector layers.
   - Integrate your data with Earth Engine operations for advanced queries.

4. **Analysis Toolkit**

   - **Air Pollutants**
   - **Urban Heat Island (UHI)** metrics
   - **Land Cover** mapping & **Change Detection**
   - Custom AI models deployed on **Vertex AI** for certain land cover tasks

5. **RAG & Knowledge Base**
   - Enables a Retrieval-Augmented Generation (RAG) workflow.
   - Upload documents to build a local knowledge base.
   - The AI Assistant can then combine geospatial insights with custom document knowledge.


## Tech Stack 💻
- Next.js
- Google Cloud Platform (GCP):
   - Google Earth Engine (remote-sensing data invocation and processing)
   - Vertex AI (custom AI vision models)
   - Cloud Run
- Vercel AI
- OpenAI (ChatGPT API)
- Supabase (database and authentication)
- LangChain (RAG)
- Turf (for spatial operations)
- Maplibre GL (for displaying maps)

## Getting Started 🚀

1. Clone the repo

2. Install dependencies

   ```bash
   npm install
   ```

3. Create a Google Earth Engine (GEE) account and project, otherwise no analysis can be done. Note that GEE is currently only free for non-commercial use:
   - https://earthengine.google.com
   
5. Set up the environment variables

- Create a `.env.local` file (or similar) with the required credentials for:

  - Google Cloud Platform (GCP):
    ```
      GOOGLE_MAPS_API_KEY           # API key for Google maps. You can replace Google Maps with OSM if you want.
      VERTEXTAI_ENDPOINT_BASE_URL   # Base URL if you use your own custom models.
      GEE_CLOUD_RUN_URL             # URL for invoking a model hosted on VertexAI using cloud functions.
      GCP_BUCKET_NAME               # Bucket name to store the land-cover map generated by your custom model (if applicable).
      GCP_SERVICE_ACCOUNT_KEY       # Service Account key needed for GEE functions, depending on your GCP configurations. Make sure it has all the required permissions to use GEE.
    ```
  - For the database & authentication, the app uses Supabase. So you need the Supabase API keys as well:

        NEXT_PUBLIC_SUPABASE_URL
        NEXT_PUBLIC_SUPABASE_ANON_KEY

  - If you want Esri integration, you also need the following keys in your env (skip this part if you don't want this integration):

        ARCGIS_CLIENT_ID=
        ARCGIS_CLIENT_SECRET=
        ARCGIS_REDIRECT_URI=

- For feedback submission, I just used a simple email-based pipeline based on Mailgun (skip this part if you don't want this feature):

        MAILGUN_API_KEY=
        MAILGUN_DOMAIN=
        RECIPIENT_EMAIL=
        SENDER_EMAIL=

5. Run the develpment server

       npm run dev


Visit http://localhost:3000 to view the application.

## How to Set up Supabase Database, Storage Bucket, & Authentication 🛢️

Supabase has a free-tier, generous plan that you can use to work with the app.

As mentioned above, the database (PostgreSQL) and authentication are both hosted on Supabase. To set up them, you can either use the local dev (https://supabase.com/docs/guides/local-development/cli/getting-started) or online (https://supabase.com/docs/guides/database/overview).
To set up the database and Supabase auth online, you need to create a supabase project & create the required databases and auth. 
You can find the database schema of the app in the `db-schema` folder.

If you want to also use the Knowledge Base feature, you need to create a storage bucket on Supabase as well. The name of the bucket should be `documents_bucket`. This is where the PDF docs you upload to the Knowledge Base are stored. You can set up the bucket by going to the following link:
 - https://supabase.com/dashboard/project/_/storage/buckets

## Available Geospatial Analyses 📊

Three sample analyses are included in this app: 
   1. urban heat island (UHI) analysis
   2. land-use/land-cover mapping (using Google DynamicWorld)
   3. land-use/land-cover change mapping (using Google DynamicWorld)
   4. air pollution analysis (not completely implemented yet)


## Considerations💡
- Note that all remote-sensing geospatial analyses, at least for now, are based on GEE in this app. So, if you don't set up your GEE environment correctly, no analysis can be done.
- It should be noted that this app is not yet ready for production. The app has known bugs, and perhaps unknown ones 😁 Some functionalities have not been implemented yet.
- I may have forgotten to include some steps in setting up the app! 😅 If there's missing information in the instructions, please open an issue and let me know to update the instructions accordingly.
- GEE-based geospatial analyses are just simple examples of how such analyses can be implemented and added. Some of them are using data that may not be up-to-date. As a result, care should be taken while interpreting the results.
- There are parts that should be refactored or re-designed either because they could have been used/invoked in a better place, or because they should've been implemented in a much better manner.


## Frequently Asked Questions (FAQ) 📌 

### 🔹 General Questions

 #### ❓ Is this project free to use?
 *Yes! This open-source version is free to use under the terms of its license. However, note that Google Earth Engine has restrictions on commercial usage.*

---

### 🔹 Support & Contributions

#### ❓ How can I get support for issues?
- *If you encounter a bug or have a feature request, please* **[open an issue](../../issues)** *on GitHub.*
- *For other questions, feel free to reach out at* **[shahabj.github@gmail.com](mailto:shahabj.github@gmail.com)**.

#### ❓ How can I contribute?
*We welcome contributions! Please check out the* **[Contributing Guidelines](./CONTRIBUTING.md)** *before submitting a pull request or opening an issue. Your help in improving this project is greatly appreciated.*

---

### 🔹 Features & Customization

 #### ❓ Can I request additional analyses or features?
   *Absolutely! You can:*
   - *Suggest a feature by opening an issue.*
   - *Fork the repository and implement your own changes.*

 *For advanced or custom solutions, please see* **[GRAI 2.0 (Enterprise Version)](#enterprise-version-grai-20)** *below.*

 #### ❓ Can I use my own geospatial datasets?
 *Yes! The app allows you to import vector data and integrate it with Google Earth Engine for custom analyses. For raster data, at least for now, you need to either host them on GEE or a GCP bucket.*

---

### 🔹 Enterprise Version: GRAI 2.0

#### ❓ What is GRAI 2.0?
*GRAI 2.0 is the enterprise version of this project, offering:*
- *Custom-built solutions tailored to specific client needs.*
- *Additional analyses & AI models not included in the open-source version.*
- *Continuous updates & premium support.*

#### ❓ How do I get access to GRAI 2.0?
*For enterprise inquiries, please visit* **[GeoRetina Contact Page](https://www.georetina.com/contact)**.

---

### 🔹 Technical & Setup Questions

#### ❓ I'm facing issues with setup. What should I do?
1. *Check that your environment variables are properly set in* `.env.local`.
2. *Check your database configurations.
3. *Confirm your Google Earth Engine configuration.*
4. *Refer to the* **[Getting Started](#getting-started)** *section in this README.*
5. *If issues persist,* **[open an issue](../../issues)**.

---

*Have a question not listed here? Feel free to* **[open an issue](../../issues)** *or reach out via email!* 🚀



