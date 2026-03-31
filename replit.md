# Workspace

## Overview

AgriAI - Smart Farming Assistant. A full-stack agricultural AI platform for Indian farmers with soil analysis, crop recommendations, leaf disease detection, AI chatbot, weather integration, and treatment recommendations.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **API framework**: Express 5
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)
- **AI**: OpenAI via Replit AI Integrations (chatbot - gpt-5-mini)
- **Frontend**: React + Vite + Tailwind CSS v4

## Features

1. **Soil Analysis** - Predict soil type, pH, fertility, moisture from NPK values
2. **Crop Recommendation** - ML-based (XGBoost/Random Forest logic) top 5 crop recommendations
3. **Leaf Disease Detection** - Detect diseases from leaf images with treatment recommendations
4. **AI Chatbot** - Multilingual farming assistant (English, Hindi, Kannada, Telugu, Tamil)
5. **Weather Integration** - Location-based weather with farming advice
6. **Treatment Recommendations** - Fertilizers, pesticides, organic solutions with dosages
7. **Datasets & Training Info** - Links to Kaggle datasets and Google Colab training notebooks

## Structure

```text
artifacts-monorepo/
├── artifacts/
│   ├── agri-ai/          # React + Vite frontend (port 20528, previewPath: /)
│   └── api-server/       # Express API server (port 8080, paths: /api)
├── lib/
│   ├── api-spec/         # OpenAPI spec + Orval codegen config
│   ├── api-client-react/ # Generated React Query hooks
│   ├── api-zod/          # Generated Zod schemas from OpenAPI
│   ├── db/               # Drizzle ORM schema + DB connection
│   └── integrations-openai-ai-server/  # OpenAI integration for chatbot
├── scripts/
└── package.json
```

## API Endpoints (all at /api)

- `GET  /api/healthz` - Health check
- `POST /api/soil/analyze` - Soil analysis (N, P, K, temp, humidity, rainfall)
- `POST /api/crops/recommend` - Crop recommendations (ML-based scoring)
- `POST /api/disease/detect` - Leaf disease detection from base64 image
- `POST /api/treatment/recommend` - Fertilizer & pesticide recommendations
- `GET  /api/weather?lat=&lon=` - Weather data for location
- `POST /api/chat/message` - AI chatbot (multilingual with OpenAI)
- `GET  /api/chat/history/:sessionId` - Chat history
- `GET  /api/datasets/info` - Kaggle dataset links + Colab notebook links

## Datasets Used (Kaggle)

1. **Crop Recommendation**: https://www.kaggle.com/datasets/atharvaingle/crop-recommendation-dataset
2. **PlantVillage (Disease)**: https://www.kaggle.com/datasets/emmarex/plantdisease
3. **Soil Images**: https://www.kaggle.com/datasets/jayaprakashpondy/soil-image-dataset
4. **Weather India**: https://www.kaggle.com/datasets/srinuti/residentialweather
5. **Fertilizer**: https://www.kaggle.com/datasets/gdabhishek/fertilizer-prediction

## Model Training (Google Colab)

- Crop Recommendation: XGBoost + Random Forest on Kaggle CSV dataset
- Disease Detection: ResNet50 transfer learning on PlantVillage
- Soil Classification: EfficientNet-B4 on soil image dataset

## TypeScript & Composite Projects

Every package extends `tsconfig.base.json`. Run `pnpm run typecheck` for full typecheck.

## Root Scripts

- `pnpm run build` — runs `typecheck` first, then recursively runs `build`
- `pnpm run typecheck` — runs `tsc --build --emitDeclarationOnly`

## Packages

### `artifacts/agri-ai` (`@workspace/agri-ai`)
React + Vite frontend with all farming assistant pages and UI.

### `artifacts/api-server` (`@workspace/api-server`)
Express 5 API server with all farming AI routes.

### `lib/db` (`@workspace/db`)
Database layer using Drizzle ORM with PostgreSQL.

### `lib/api-spec` (`@workspace/api-spec`)
OpenAPI 3.1 spec and Orval codegen config.

### `lib/integrations-openai-ai-server` (`@workspace/integrations-openai-ai-server`)
OpenAI integration for the AI chatbot (uses Replit AI Integrations).
