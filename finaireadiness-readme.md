# 🛡️ FinAIReadiness - AI Risk Assessment Tool

A modern web application built with Next.js that evaluates AI systems against industry-standard governance frameworks using intelligent analysis to provide comprehensive risk assessment and actionable recommendations.



## 🚀 Features

- **Interactive Assessment Questionnaire**: Step-by-step evaluation of AI systems completed by product teams
- **Dual Assessment Paths**: 
  - Standard assessment for first-time users
  - Gap analysis for users with existing risk implementations (21-question checklist)
- **AI-Powered Risk Analysis**: Uses OpenAI to provide intelligent compliance scoring against industry frameworks
- **Comprehensive Risk Categories**: Evaluates Hallucination, Prompt Injection, and Data Leakage risks
- **Actionable Recommendations**: Provides specific mitigation strategies based on industry best practices
- **Professional Report Generation**: Download detailed assessment reports as PDF files
- **Email Integration**: Send reports directly to product managers via Gmail API
- **Modern Responsive UI**: Clean interface with Tailwind CSS and percentage-based risk scoring

## 🏗️ Architecture

```
FinAIReadiness/
├── apps/web/                 # Next.js application
│   ├── src/
│   │   ├── app/              # App router pages and API routes
│   │   ├── components/       # React components
│   │   └── utils/            # Risk analysis and gap analysis logic
│   └── data/                 # Industry framework JSON files
├── data/                     # Framework reference data
└── README.md
```

## 🛠️ Tech Stack

- **Frontend**: Next.js 14, React 18, TypeScript, Tailwind CSS
- **Backend**: Next.js API Routes, OpenAI GPT-4o-mini
- **PDF Generation**: jsPDF + html2canvas
- **Email**: Gmail API integration
- **Deployment**: Vercel-ready
- **Framework**: Industry-standard AI governance framework

## 🔧 Local Development

### Prerequisites

- Node.js 18+
- OpenAI API key
- Gmail API credentials (optional, for email features)

### Quick Start

1. **Clone the repository**
   ```bash
   git clone https://github.com/finos-labs/dtcc-i-h-2025-finaireadiness.git
   cd dtcc-i-h-2025-finaireadiness
   ```

2. **Install dependencies**
   ```bash
   npm install
   cd apps/web && npm install
   ```

3. **Set up environment variables**
   ```bash
   cd apps/web
   cp .env.example .env.local
   ```
   
   Edit `.env.local` and add:
   ```env
   OPENAI_API_KEY=sk-your-openai-key-here
   ```

4. **Set up Gmail Integration (For mailing the generated report)**
   
   **For Local Development:**
   
   1. **Enable Gmail API** in Google Cloud Console
   2. **Create OAuth2 credentials** for your application
   3. **Configure OAuth consent screen**
   4. **Generate and download credentials**
   5. **Create `token.json`** in the project root:
   
   ```json
   {
     "access_token": "ya29.your-access-token",
     "refresh_token": "1//your-refresh-token", 
     "token_uri": "https://oauth2.googleapis.com/token",
     "client_id": "your-client-id.apps.googleusercontent.com",
     "client_secret": "your-client-secret",
     "scopes": [
       "https://www.googleapis.com/auth/gmail.send"
     ]
   }
   ```
   
   **⚠️ Security Note**: Never commit `token.json` to version control!

4. **Run the development server**
   ```bash
   npm run dev
   ```

5. **Open your browser**
   Visit `http://localhost:3000`

## 📧 Gmail Integration Setup

### For Local Development

1. **Go to Google Cloud Console** → [console.cloud.google.com](https://console.cloud.google.com)
2. **Create or select a project**
3. **Enable Gmail API**:
   - Go to "APIs & Services" → "Library"
   - Search for "Gmail API" and enable it
4. **Create OAuth2 credentials**:
   - Go to "APIs & Services" → "Credentials"
   - Click "Create Credentials" → "OAuth 2.0 Client IDs"
   - Choose "Web application"
   - Add authorized redirect URIs if needed
5. **Configure OAuth consent screen**:
   - Go to "OAuth consent screen"
   - Fill in required information
   - Add your email to test users
6. **Download credentials** and extract:
   - `client_id`
   - `client_secret`
7. **Generate tokens** (requires OAuth flow implementation)
8. **Create `token.json`** in project root with your credentials

### For Vercel Deployment

1. **In Vercel Dashboard**:
   - Go to your project settings
   - Navigate to "Environment Variables"
2. **Add the following variables**:
   ```
   GMAIL_CLIENT_ID=your-client-id
   GMAIL_CLIENT_SECRET=your-client-secret
   GMAIL_ACCESS_TOKEN=your-access-token
   GMAIL_REFRESH_TOKEN=your-refresh-token
   ```
3. **The app will use environment variables** instead of `token.json` file
4. **Redeploy** your application

### Alternative: Disable Email Features

If you don't need email functionality:
- Simply don't create `token.json`
- Don't set Gmail environment variables  
- The app will work without email features

## 🌐 Deployment

This application is optimized for deployment on Vercel:

### Deploy with Vercel

1. **Fork this repository**
2. **Connect to Vercel**:
   - Go to [vercel.com](https://vercel.com)
   - Click "New Project"
   - Import your GitHub repository
   - Select the `apps/web` directory as the root
3. **Add Environment Variables**:
   - `OPENAI_API_KEY`: Your OpenAI API key (required)
   - `GMAIL_CLIENT_ID`: Gmail OAuth client ID (optional)
   - `GMAIL_CLIENT_SECRET`: Gmail OAuth client secret (optional)
   - `GMAIL_ACCESS_TOKEN`: Gmail access token (optional)
   - `GMAIL_REFRESH_TOKEN`: Gmail refresh token (optional)
4. **Deploy**: Vercel will automatically build and deploy

### Environment Variables Required

| Variable | Description | Required |
|----------|-------------|----------|
| `OPENAI_API_KEY` | OpenAI API key for AI analysis | Yes |
| `GMAIL_CLIENT_ID` | Gmail OAuth client ID | No |
| `GMAIL_CLIENT_SECRET` | Gmail OAuth client secret | No |
| `GMAIL_ACCESS_TOKEN` | Gmail access token | No |
| `GMAIL_REFRESH_TOKEN` | Gmail refresh token | No |

**Note**: Gmail integration is optional. The tool works fully without email features.

## 📊 How It Works

### Assessment Process

1. **Product Information Collection**: Product name, manager details, and system configuration
2. **Risk Assessment Path Selection**:
   - **Standard Assessment**: For first-time users - comprehensive AI analysis
   - **Gap Analysis**: For users with existing implementations - 21-question compliance checklist
3. **Intelligent Risk Analysis**: AI evaluates system against industry framework criteria
4. **Results Generation**: 
   - Overall risk percentage (calculated as average of individual risk scores)
   - Individual risk category scores (Hallucination, Prompt Injection, Data Leakage)
   - Compliance assessment with specific recommendations
5. **Professional Reporting**: Generate and download PDF reports or email to stakeholders

### Supported Risk Categories

- **Hallucination and Inaccurate Outputs**: Accuracy and output reliability concerns
- **Prompt Injection**: Security and input validation vulnerabilities  
- **Information Leaked to Hosted Models**: Privacy and data protection risks

## 🎯 Framework Integration

### Risk Assessment Methodology

The tool evaluates AI systems based on:
- AI model deployment type (self-hosted, API-based, third-party cloud)
- Use case categorization (customer service, document analysis, etc.)
- Data sensitivity levels (public, internal, confidential, restricted)
- Accuracy requirements (low, moderate, high, critical)
- Industry context and regulatory requirements

### Scoring System

- **Risk Scores**: 20-80 scale where higher scores indicate higher risk
- **Overall Risk**: Calculated as average of applicable individual risk scores
- **Risk Levels**: 
  - 20-35: Low Risk
  - 35-55: Medium Risk  
  - 55-80: High Risk
- **Display**: All scores shown as percentages for intuitive understanding

### External Standards Referenced

- **OWASP LLM Top 10** - LLM Application Security Standard
- **FFIEC Guidelines** - Financial Institution IT Examination
- **EU AI Act** - European AI Regulation Framework
- **NIST AI RMF** - AI Risk Management Framework

## 🔒 Security & Privacy

- Environment variables for sensitive data protection
- No client-side storage of API keys
- Input validation and sanitization
- Gmail OAuth2 authentication
- Industry framework compliance
- Comprehensive .gitignore for credential protection

### Protected Files

The following files are automatically ignored by git for security:
- `token.json` - Gmail API credentials (local development)
- `.env.local` - Environment variables with API keys

**⚠️ Important**: Never commit these files to version control!

## 📁 Project Structure

```
apps/web/
├── src/
│   ├── app/
│   │   ├── api/
│   │   │   ├── assess/route.ts          # Main assessment API
│   │   │   ├── send-email/route.ts      # Email integration
│   │   │   └── framework-data/route.ts  # Framework data access
│   │   ├── layout.tsx                   # App layout
│   │   └── page.tsx                     # Main page with state management
│   ├── components/
│   │   ├── AssessmentForm.tsx           # Main questionnaire form
│   │   ├── ChecklistAssessment.tsx      # Gap analysis checklist
│   │   ├── ResultsDisplay.tsx           # Results and PDF generation
│   │   └── checklistData.ts            # Checklist configuration
│   └── utils/
│       └── gapAnalysis.ts              # Gap analysis calculations
├── data/                               # Framework JSON files
└── package.json                       # App dependencies
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Industry-standard AI governance frameworks for risk assessment methodology
- **OpenAI** for AI analysis capabilities
- **Vercel** for hosting and deployment platform
- **OWASP** for LLM security standards
- **FINOS** for AI governance framework foundations

## 📞 Support

For questions or issues:
- Create an issue in this repository
- Review the setup documentation in `/docs` folder
- Check OpenAI API documentation for integration issues

---

**Built for Enterprise AI Governance** 🏆

This tool demonstrates practical application of industry-standard governance frameworks with modern AI capabilities for intelligent compliance assessment and risk management.

## 🚀 Quick Commands

```bash
# Development
npm run dev                 # Start development server
npm run build              # Build for production
npm run start              # Start production server

# Setup
npm run install:all        # Install all dependencies
npm run setup              # Complete setup with PDF and email dependencies
```