# My Own ChatGPT Clone

This repository contains the code for a personal ChatGPT clone built using Assistant UI and the Google Gemini API. This project allows you to interact with the powerful Gemini language model through a simple web interface.

## Prerequisites

Before you can run or understand this project, ensure you have the following installed:

* **VS Code:** You can download it from the official Visual Studio Code website.
* **Node.js:** (version 18 or later recommended) You can download it from the official Node.js website. `npm` comes bundled with Node.js.
* **Google AI Studio API Key:** You'll need to obtain an API key from the Google AI Studio platform.
* **GitHub Account:** You'll need an account on the GitHub platform.
* **Vercel Account:** You'll need an account on the Vercel platform.

## Setup and Deployment

Follow these steps to create and deploy your own version of this application:

1.  **Clone the Repository (Optional):** If you haven't already, clone this repository to your local machine.

2.  **Create Project Folder:** Create a folder named `ChatGpt` on your computer.

3.  **Open in VS Code:** Open the `ChatGpt` folder in Visual Studio Code.

4.  **Initialize Assistant UI:** Open the terminal in VS Code and run the following command:

    ```bash
    npx assistant-ui@latest create
    ```

5.  **Navigate to Project Directory:** Change your current directory to the newly created `my-app` folder:

    ```bash
    cd my-app
    ```

6.  **Install Dependencies:** Install the necessary SDKs:

    ```bash
    npm install ai @assistant-ui/react-ai-sdk @ai-sdk/google
    ```

7.  **Configure API Route:**
    * Navigate to the file `/app/api/chat/route.ts`.
    * Clear the contents of this file.
    * Paste the following code:

        ```typescript
        import { google } from "@ai-sdk/google";
        import { streamText } from "ai";

        export const maxDuration = 30;

        export async function POST(req: Request) {
          const { messages } = await req.json();
          const result = streamText({
            model: google("gemini-2.0-flash"),
            messages,
          });
          return result.toDataStreamResponse();
        }
        ```

8.  **Set Up Environment Variable:**
    * Create a new file named `.env.local` in the root of your `my-app` directory.
    * Add your Google AI Studio API key to this file:

        ```
        GOOGLE_GENERATIVE_AI_API_KEY="YOUR_API_KEY"
        ```

        **Important:** Replace `"YOUR_API_KEY"` with your actual API key.

9.  **Run Development Server:** Start the development server:

    ```bash
    npm run dev
    ```

    Your application should now be running locally. You can usually access it by clicking on the link displayed in the terminal (typically `http://localhost:3000`).

10. **Build for Production:** Once you're satisfied with your local setup, build the production-ready code:

    ```bash
    npm run build
    ```

11. **Clean Up (Optional):** You can now delete the `node_modules` folder and the `.env.local` file as the API key will be configured in Vercel.

12. **Push to GitHub:**
    * Create a new repository on GitHub named **`chatgpt_clone`**.
    * Upload the contents of your **`my-app`** folder to this repository. You can do this by dragging and dropping the folder into the GitHub web interface or by using Git commands as shown in the video you followed.

13. **Deploy to Vercel:**
    * Create an account on the Vercel platform.
    * Connect your GitHub account to Vercel.
    * Create a new project in Vercel and select your **`chatgpt_clone`** repository.
    * **Important:** When configuring the project in Vercel, make sure you select the **`my-app`** folder as the root directory for deployment. Also, ensure the framework is set to **Next.js**.
    * Add your Google AI Studio API key as an environment variable in your Vercel project settings. The key should be named `GOOGLE_GENERATIVE_AI_API_KEY` and the value should be your actual API key.

14. **Wait for Deployment:** Vercel will now build and deploy your application. This process might take a few minutes.

15. **Access Your Live Website:** Once the deployment is complete, Vercel will provide you with a unique URL where your ChatGPT clone is live and accessible.

## Disclaimer

This project is a personal implementation and may have limitations compared to the full-fledged ChatGPT. It utilizes the Google Gemini API, and its capabilities and limitations are subject to the terms and conditions of Google AI Studio.

