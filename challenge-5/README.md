# Challenge 5: Claims Processing UI

**Expected Duration:** 30 minutes

## Introduction

Welcome to Challenge 5! In this challenge, you'll build a user-friendly web interface using **Streamlit** to consume the Claims Processing API you deployed in Challenge 4. This UI will allow users to upload insurance claim images and view the structured results extracted by the multi-agent workflow—completing the end-to-end claims processing solution.

## What are we building?

In this challenge, you will create:

- **Streamlit Web App**: A simple, interactive UI for uploading and processing claim images
- **API Integration**: Connect to the Challenge 4 REST API to process claims
- **Results Display**: Parse and display structured claim data (vehicle info, damage assessment, incident details)
- **Session History**: Track all processed claims during your session

## Architecture

```
┌──────────────────────────────────┐
│     Streamlit UI (this app)      │
│     http://localhost:8501        │
└──────────────┬───────────────────┘
               │
               │ HTTP REST API
               │
┌──────────────▼───────────────────┐
│   Azure API Management (APIM)    │
│      MCP Server Endpoint         │
│  https://<apim>.azure-api.net/...│
└──────────────┬───────────────────┘
               │
┌──────────────▼───────────────────┐
│     Claims Processing API        │
│     Azure Container Apps         │
└──────────────────────────────────┘
```

## Quick Start

### 1. Install Dependencies

```bash
cd challenge-5-ui
pip install -r requirements.txt
```

### 2. Get your MCP Server URL from Challenge 4

Use the **MCP Server URL** created in Challenge 4 Task 6.4 through Azure API Management:

```bash
# Your MCP Server URL should look like:
# https://<your-apim-name>.azure-api.net/<api-path>
```

You can find this URL in the Azure Portal:
1. Go to **API Management** → Your APIM instance
2. Navigate to **MCPs** section
3. Copy the **MCP Server URL**

### 3. Start the Streamlit UI

```bash
cd challenge-5-ui
API_URL=https://<your-apim-name>.azure-api.net/<api-path> streamlit run app.py
```

Or configure the API URL in the sidebar after launching:

```bash
streamlit run app.py
```

### 4. Open in Browser

Navigate to http://localhost:8501

## Usage

1. **Configure API URL**: In the sidebar, paste your MCP Server URL from APIM
2. **Check Health**: Click "Check API Health" to verify connectivity
3. **Upload Image**: Use the file uploader to select a claim image
4. **Process**: Click "Process Claim" to send the image to the API
5. **View Results**: See the structured claim data displayed in a user-friendly format

## UI Tabs

### 📤 Upload Claim
- File uploader for claim images
- Preview of uploaded image
- Choice of processing method (file upload vs base64)
- Results display with structured data

### 📊 Results History
- View all previously processed claims
- Each result can be expanded for details
- Clear history option

### 🔧 Debug
- Session state inspection
- Last result viewer
- Manual API testing tool

## Configuration

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `API_URL` | Claims Processing API URL | `http://localhost:8000` |

### Sidebar Settings

- **API URL**: Can be changed dynamically in the sidebar
- **Health Check**: Test API connectivity


## Development

### Extending the UI

To add new features:

1. Add new tabs in the `tabs` section of `main()`
2. Create helper functions for API calls
3. Use Streamlit components for display

## Conclusion

Congratulations! 🎉 You've successfully built a complete end-to-end claims processing solution:

1. **Challenge 0-3**: Built the AI agents for document processing, OCR, and data extraction
2. **Challenge 4**: Deployed the multi-agent workflow as a REST API on Azure Container Apps
3. **Challenge 5**: Created a user-friendly web interface to interact with the API

Your Streamlit UI now allows users to easily upload claim images and receive structured data extracted by your AI-powered backend.

### Next Steps

Ready to take it further? Consider deploying this Streamlit UI to **Azure Container Apps** for a fully cloud-hosted solution:

```bash
# Create a Dockerfile for the Streamlit app
# Build and push to Azure Container Registry
# Deploy to Azure Container Apps

az containerapp create \
  --name claims-processing-ui \
  --resource-group <your-rg> \
  --environment <your-environment> \
  --image <your-acr>.azurecr.io/claims-ui:latest \
  --target-port 8501 \
  --ingress external
```

This would give you a production-ready, scalable UI that complements your backend API!

## Related

- [Challenge 4: API Server](../challenge-4/README.md)
- [Streamlit Documentation](https://docs.streamlit.io/)
- [Deploy Streamlit to Azure Container Apps](https://learn.microsoft.com/azure/container-apps/)
