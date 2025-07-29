# Tech Stack - Woppa MVP

Confirmed technology decisions for Woppa MVP development.

## Mobile Application
- **Framework**: React Native 0.80+
- **Language**: TypeScript
- **Platforms**: Android + iOS
- **State Management**: 
  - TanStack Query (React Query) for server state management
  - Zustand for client state management
- **Reasoning**: Hybrid development to reduce time and costs while maintaining native performance

## Mobile Development Enhancements
- **Navigation**: Expo Router (file-based routing)
- **Image Handling**: Expo Image (optimized image component with caching)
- **Styling**: NativeWind (Tailwind CSS for React Native)
- **Reasoning**: Specialized tools that enhance developer experience, improve app performance, and provide modern development patterns while maintaining Expo ecosystem compatibility

## Web Panel
- **Framework**: React 19+ with TypeScript
- **UI Components**: shadcn/ui
- **State Management**: 
  - TanStack Query (React Query) for server state management
  - Zustand for client state management
- **Reasoning**: Mature ecosystem, team experience, and compatibility with UI generation tools

## Backend & Database
- **Runtime**: Node.js 24+
- **Database**: PostgreSQL 17+
- **ORM**: Prisma
- **Reasoning**: Modern JavaScript runtime with robust relational database and type-safe ORM

## Development Tools
- **Code Formatting**: Prettier
- **Testing**: Vitest
- **Build Tool**: Vite

## External Services
- **Authentication**: Google OAuth 2.0
- **Maps & Geolocation**: 
  - Google Maps API
  - Google Places API (address autocomplete)

## Compliance
- **Data Protection**: LGPD (General Data Protection Law of Brazil)

## Pending Decisions
- Backend framework (Express.js vs alternatives)
- Authentication system (Firebase Auth vs direct Google OAuth)
- SMS validation service (Twilio vs Brazilian providers like Zenvia, TotalVoice)
- Payment processing system
- Push notifications service
- Admin panel solution (considering AdminJS)

---
*Document updated: 2025-01-24*