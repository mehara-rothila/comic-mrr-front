# Comic Portal Frontend

## Project Overview
Comic Portal is a comprehensive web-based comic management platform built with Vue.js. It provides sophisticated user authentication, CRUD operations for comics, and a dynamic user interface with Role-Based Access Control (RBAC).

## Features
- User Authentication (Login/Register)
- Comic Management (Create, Read, Update, Delete)
- Role-Based Access Control (Admin/User)
- Dynamic Category System
- Administrative Dashboard
- Personal Comic Collection Management
- Real-time Form Validation
- Enhanced Error Handling

## Project Structure
```
src/
├── assets/           # Static resources
├── components/       # Reusable Vue components
│   ├── ComicFormModal.vue  # Comic management interface
│   └── LoadingState.vue    # Loading state handlers
├── config/
│   └── categories.js # Category definitions and styling
├── router/
│   └── index.js     # Route configurations
├── services/
│   └── api.js       # API service integration
├── stores/
│   ├── auth.js      # Authentication state management
│   └── comic.js     # Comic state management
└── views/
    ├── HomeView.vue      # Main landing interface
    ├── Login.vue         # Authentication interface
    ├── Register.vue      # User registration
    ├── AdminPanel.vue    # Administrative dashboard
    ├── ComicList.vue     # Comics catalog
    ├── ComicDetail.vue   # Individual comic view
    ├── MyComics.vue      # Personal collection
    └── NotFound.vue      # Error handling
```

## Prerequisites
- Node.js (v14 or higher)
- npm or yarn
- Backend API server running (See [Backend Repository](https://github.com/mehara-rothila/comic-mrr-backend))

## Installation

1. Clone the repository:
```bash
git clone https://github.com/mehara-rothila/comic-mrr-front.git
cd comic-mrr-front
```

2. Install dependencies:
```bash
npm install
```

3. Create environment file:
```bash
echo "VITE_API_URL=http://localhost:8000/api" > .env
```

4. Run development server:
```bash
npm run dev
```

## Available Scripts
- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run preview` - Preview production build

## Configuration
The application can be configured via environment variables:
- `VITE_API_URL` - Backend API URL

## Category System
The system includes predefined categories with color coding:
- Action & Adventure (Blue)
- Fantasy & Magic (Purple)
- Superhero (Red)
- Slice of Life (Green)
- Mystery & Horror (Gray)
- Romance (Pink)
- Sci-Fi (Indigo)
- Comedy (Yellow)

## Administrative Access
Default admin credentials for testing:
```
Email: admin3@admin.com
Password: password
```

## Features in Development
- Media upload functionality
- Search system implementation
- Content filtering
- User preference system
- Enhanced error management

## Contributing
1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License
This project is licensed under the MIT License - see the LICENSE file for details.

## Contact
Mehara Rothila - [GitHub](https://github.com/mehara-rothila)

Project Link: [https://github.com/mehara-rothila/comic-mrr-front](https://github.com/mehara-rothila/comic-mrr-front)
