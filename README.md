# DocSummary AI - Document Summary Assistant

A complete, professional, full-stack web application that transforms documents into intelligent AI-powered summaries with OCR capabilities, highlights, and actionable insights.

## Features

### Core Functionality
- **Document Upload**: Drag-and-drop or file picker for PDFs and images (PNG, JPG, JPEG, TIFF)
- **Text Extraction**:
  - Native PDF text extraction with structure preservation
  - Advanced OCR for images using Tesseract (simulated in demo)
- **AI-Powered Summaries**:
  - Three length options: Short (50-100 words), Medium (150-250 words), Long (350-600 words)
  - Customizable focus tags for targeted summaries
  - Automatic highlight extraction with page references
  - Improvement suggestions
- **Document History**: View, re-access, and manage previously processed documents
- **User Authentication**: Secure email/password authentication with Supabase
- **Admin Dashboard**: System metrics, user activity monitoring, and feedback analysis

### UI/UX Highlights
- Modern, responsive design optimized for mobile, tablet, and desktop
- Smooth animations and transitions
- Professional color palette with gradients
- Real-time progress tracking for uploads and processing
- Side-by-side source text and summary viewing
- Multiple download formats (TXT, Markdown)

### Security Features
- Row-level security (RLS) on all database tables
- Encrypted file storage
- Authentication-protected routes
- Secure API endpoints with JWT verification

## Tech Stack

### Frontend
- React 18 with TypeScript
- Tailwind CSS for styling
- Vite for build tooling
- Lucide React for icons

### Backend
- Supabase (PostgreSQL database)
- Supabase Edge Functions (serverless)
- Supabase Storage for file management
- Supabase Auth for authentication

### AI & Processing
- Mock AI summary generation (ready for OpenAI integration)
- Simulated OCR processing (ready for Tesseract.js integration)
- PDF text extraction pipeline

## Project Structure

```
project/
├── src/
│   ├── components/          # Reusable UI components
│   │   ├── Navbar.tsx
│   │   ├── Footer.tsx
│   │   └── LoadingSpinner.tsx
│   ├── pages/              # Main application pages
│   │   ├── HomePage.tsx
│   │   ├── AuthPage.tsx
│   │   ├── UploadPage.tsx
│   │   ├── GenerateSummaryPage.tsx
│   │   ├── SummaryResultPage.tsx
│   │   ├── HistoryPage.tsx
│   │   ├── AboutPage.tsx
│   │   └── AdminPage.tsx
│   ├── contexts/           # React contexts
│   │   └── AuthContext.tsx
│   ├── lib/               # Utilities and configurations
│   │   └── supabase.ts
│   ├── App.tsx            # Main application component
│   └── main.tsx           # Application entry point
├── supabase/
│   └── functions/         # Edge Functions
│       ├── upload-file/
│       ├── extract-text/
│       └── generate-summary/
└── README.md
```

## Getting Started

### Prerequisites
- Node.js 18+ and npm
- Supabase account and project

### Installation

1. **Clone and install dependencies**
   ```bash
   npm install
   ```

2. **Set up Supabase**
   - Create a new Supabase project at https://supabase.com
   - The database migration has already been applied
   - Create a storage bucket named `documents`:
     - Go to Storage in Supabase dashboard
     - Click "New bucket"
     - Name: `documents`
     - Public: No (private)
     - Click "Create bucket"

3. **Configure environment variables**

   Create a `.env` file in the project root:
   ```env
   VITE_SUPABASE_URL=your_supabase_project_url
   VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
   ```

   Get these values from your Supabase project settings.

4. **Run the development server**
   ```bash
   npm run dev
   ```

   The application will be available at http://localhost:5173

### Building for Production

```bash
npm run build
```

The production-ready files will be in the `dist/` directory.

## Database Schema

### Tables
- **profiles**: User profiles with admin flags
- **files**: Uploaded document metadata
- **extractions**: Text extraction results with page data
- **summaries**: AI-generated summaries with highlights
- **history**: User document history
- **feedback**: User ratings and comments

All tables have Row Level Security (RLS) enabled with appropriate policies.

## Edge Functions

### upload-file
Handles file uploads with validation and storage.
- Validates file type and size
- Uploads to Supabase Storage
- Creates database record

### extract-text
Processes documents to extract text.
- Native PDF text extraction
- OCR for images
- Page-by-page processing
- Structured output with metadata

### generate-summary
Generates AI-powered summaries.
- Multiple length options
- Focus tag support
- Highlight extraction
- Improvement suggestions

## Usage Guide

### For Regular Users

1. **Sign Up/Sign In**
   - Click "Sign In" in the navigation
   - Create an account or sign in with existing credentials

2. **Upload a Document**
   - Navigate to "Upload"
   - Drag and drop a file or click "Browse Files"
   - Supported formats: PDF, PNG, JPG, JPEG, TIFF (max 50MB)
   - Wait for upload and text extraction

3. **Generate Summary**
   - Choose summary length: Short, Medium, or Long
   - (Optional) Add focus tags like "action items, key findings"
   - Click "Generate Summary"

4. **View Results**
   - Read the AI-generated summary
   - Review highlights with page references
   - Check improvement suggestions
   - Copy, download, or regenerate summary
   - Toggle source text view for reference
   - Rate the summary

5. **Access History**
   - View all processed documents
   - Re-open previous summaries
   - Delete unwanted items

### For Administrators

1. **Access Admin Dashboard**
   - Only users with `is_admin = true` can access
   - Navigate to "Admin" in the navigation

2. **View Metrics**
   - Total users, documents, and summaries
   - Average user rating
   - Recent uploads and feedback
   - System status

## Customization

### Adding Real AI Integration

To integrate with OpenAI or another LLM:

1. Update `supabase/functions/generate-summary/index.ts`
2. Add OpenAI API calls instead of mock generation
3. Set environment variable in Supabase Edge Functions settings

### Adding Real OCR

To integrate with Tesseract or cloud OCR:

1. Update `supabase/functions/extract-text/index.ts`
2. Add Tesseract.js or cloud OCR API
3. Implement image preprocessing

### Styling

The application uses Tailwind CSS. Customize colors in `tailwind.config.js`:

```javascript
theme: {
  extend: {
    colors: {
      // Add custom colors
    }
  }
}
```

## Security Considerations

- All database operations use RLS policies
- File uploads are validated on both client and server
- Authentication required for document processing
- Admin endpoints check user permissions
- Files stored in private storage bucket
- JWT tokens for API authentication

## Performance Optimization

- Images use CDN (Pexels)
- Lazy loading for images
- Optimized build with Vite
- Code splitting by route
- Database indexes on frequently queried columns

## Troubleshooting

### Build Errors
```bash
npm run typecheck
```

### Database Issues
- Verify RLS policies are enabled
- Check user permissions
- Ensure storage bucket exists

### Upload Failures
- Check file size (max 50MB)
- Verify file type is supported
- Ensure storage bucket is configured

## Future Enhancements

- Real-time collaboration
- Document comparison
- Custom AI models
- Batch processing
- API access for integrations
- Mobile app
- Advanced analytics

## License

This project is provided as-is for educational and commercial use.

## Support

For issues or questions, please check:
- Database configuration in Supabase dashboard
- Environment variables in `.env`
- Browser console for errors
- Network tab for API failures

---

Built with React, TypeScript, Tailwind CSS, and Supabase.
