# 🌟 Aira Smart Perfume System

> **AI-Powered Adaptive Fragrance Technology**  
> Revolutionary smart perfume bottle that dynamically blends over 1 million unique scent combinations using artificial intelligence and precision microfluidics.

[![License](https://img.shields.io/badge/License-Proprietary-red.svg)](LICENSE)
[![Patent](https://img.shields.io/badge/Patent-Pending-yellow.svg)](https://saip.gov.sa)
[![Platform](https://img.shields.io/badge/Platform-iOS%20%7C%20Android-blue.svg)](https://reactnative.dev/)
[![AI](https://img.shields.io/badge/AI-Claude%20Sonnet%204-purple.svg)](https://anthropic.com)

---

## 📋 Project Overview

**Aira** is a next-generation smart perfume system that combines advanced **microfluidics**, **AI-driven personalization**, and **IoT connectivity** to create a truly adaptive fragrance experience. Unlike traditional perfumes with static compositions, Aira dynamically mixes base fragrance concentrates in real-time based on:

- **User mood and preferences** (analyzed via AI)
- **Environmental context** (time, weather, location, activity)
- **Historical usage patterns** (ML-powered recommendations)

The system consists of:
1. **Smart Bottle** - IoT-enabled device with 12 replaceable fragrance cartridges
2. **Mobile Application** - Cross-platform interface for personalization and control
3. **AI Engine** - Claude API integration for intelligent scent recommendation
4. **Cloud Backend** - Recipe storage, analytics, and over-the-air updates

---

## ✨ Core Features

### 🎨 Dynamic Fragrance Mixing
- **1,000,000+ unique combinations** from 12-20 base concentrates
- **Precision dispensing** with ±0.05ml accuracy using peristaltic micro-pumps
- **Ultrasonic mixing chamber** (40kHz) for homogeneous blending in 2-3 seconds
- **Real-time formulation** based on AI recommendations or custom user recipes

### 🤖 AI-Powered Personalization
- **Claude API integration** (Anthropic Sonnet 4) for context-aware recommendations
- **Mood-based selection**: Happy, Calm, Energetic, Professional, Romantic
- **Adaptive learning**: Improves recommendations based on user ratings and usage patterns
- **Contextual awareness**: Time of day, weather conditions, location, and activity type

### 📱 Mobile Application
- **Cross-platform**: React Native for iOS 13+ and Android 8+
- **Premium UI/UX**: Luxury dark theme with gold accents and refined typography
- **Custom formula creator**: Interactive sliders with real-time composition visualization
- **Recipe library**: Save, share, and discover fragrance formulas
- **Device management**: Battery monitoring, cartridge levels, firmware updates

### 🔐 Security & Authentication
- **RFID cartridge verification**: Prevents counterfeit refills
- **AES-256 encryption**: Secure data transmission
- **OAuth 2.0 + Biometric auth**: Face ID / Touch ID / Fingerprint
- **Optional blockchain tracking**: Supply chain transparency

### 🌱 Sustainability
- **90% waste reduction**: Reusable bottle with replaceable cartridges
- **Eco-friendly materials**: Medical-grade silicone, food-grade PTFE, borosilicate glass
- **Smart refill system**: Auto-reordering when cartridges run low

---

## 🛠️ Technical Stack

### **Hardware Components**
| Component | Specification | Purpose |
|-----------|--------------|---------|
| **Microcontroller** | ESP32-WROOM-32 (Dual-core 240MHz, 520KB RAM) | Main processing unit |
| **Connectivity** | Bluetooth 5.0 BLE + WiFi 6 | App communication & cloud sync |
| **Micro-Pumps** | 12x Peristaltic pumps (0.1-10 ml/min, ±0.05ml accuracy) | Precision dispensing |
| **RFID Reader** | MFRC522 (13.56MHz) | Cartridge authentication |
| **Sensors** | DHT22 (temp/humidity), MPU6050 (6-axis IMU), Capacitive level sensors | Context awareness |
| **Mixing System** | Ultrasonic transducer (40kHz, 10W) | Homogeneous blending |
| **Battery** | Li-Po 3.7V 3000mAh + Qi wireless charging | ~300 dispenses per charge |
| **Display** | OLED 0.96" 128x64 I2C | Status indicators |

### **Software Stack**

#### **Mobile Application**
```
Frontend:        React Native (Cross-platform)
State Management: Redux Toolkit + Redux Persist
Navigation:      React Navigation 6.x
UI Components:   Custom components + React Native Paper
Animations:      React Native Reanimated 2
Charts:          Victory Native (usage analytics)
Styling:         Styled Components
HTTP Client:     Axios + React Query
Bluetooth:       React Native BLE Manager
```

#### **Backend Services**
```
Runtime:         Node.js 18+ (LTS)
Framework:       Express.js 4.x
Database:        PostgreSQL 14+ (user data, recipes, analytics)
Caching:         Redis 7+ (session management, rate limiting)
ORM:             Prisma 4.x
Authentication:  Passport.js (OAuth 2.0, JWT)
File Storage:    AWS S3 / Azure Blob (firmware updates, user avatars)
Push Notifications: Firebase Cloud Messaging (FCM)
Analytics:       Mixpanel / Amplitude
```

#### **AI & ML Services**
```
AI Engine:       Claude API (Anthropic Sonnet 4)
ML Models:       TensorFlow Lite (on-device inference for offline mode)
Recommendation:  Collaborative Filtering + Content-based hybrid
Training:        Python 3.11 + scikit-learn + pandas
```

#### **Firmware (Embedded)**
```
Language:        C/C++ (Arduino framework)
RTOS:            FreeRTOS (task scheduling)
Communication:   MQTT (lightweight messaging)
OTA Updates:     ESP32 OTA library
Storage:         SPIFFS (file system for configs)
```

#### **DevOps & Infrastructure**
```
CI/CD:           GitHub Actions
Containerization: Docker + Docker Compose
Cloud Platform:  AWS / Azure / GCP
Monitoring:      Grafana + Prometheus
Logging:         ELK Stack (Elasticsearch, Logstash, Kibana)
API Gateway:     Kong / AWS API Gateway
```

---

## 🏗️ System Architecture

### High-Level Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         MOBILE APP (React Native)                │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐          │
│  │   Home UI    │  │  AI Selector │  │ Formula Maker│          │
│  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘          │
│         │                  │                  │                   │
│         └──────────────────┴──────────────────┘                  │
│                            │                                      │
└────────────────────────────┼──────────────────────────────────────┘
                             │
                    ┌────────▼────────┐
                    │   REST API      │
                    │  (Express.js)   │
                    └────────┬────────┘
                             │
         ┌───────────────────┼───────────────────┐
         │                   │                   │
    ┌────▼─────┐      ┌─────▼──────┐     ┌─────▼──────┐
    │PostgreSQL│      │   Redis    │     │ Claude API │
    │ (Recipes)│      │  (Cache)   │     │ (AI Engine)│
    └──────────┘      └────────────┘     └────────────┘
                             │
                    ┌────────▼────────┐
                    │   BLE Gateway   │
                    │  (MQTT Bridge)  │
                    └────────┬────────┘
                             │
┌────────────────────────────▼──────────────────────────────────────┐
│                      SMART BOTTLE (ESP32)                          │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐           │
│  │ Pump Control │  │ RFID Reader  │  │  Sensors     │           │
│  │ (12x PWM)    │  │ (Auth)       │  │ (Context)    │           │
│  └──────┬───────┘  └──────────────┘  └──────────────┘           │
│         │                                                          │
│         ▼                                                          │
│  ┌─────────────────────────────────────────────────┐             │
│  │      Mixing Chamber (Ultrasonic 40kHz)          │             │
│  └─────────────────────────────────────────────────┘             │
│                           │                                        │
│                           ▼                                        │
│                  [ Atomizer Output ]                               │
└────────────────────────────────────────────────────────────────────┘
```

### Communication Flow

1. **User Interaction** → Mobile app captures mood/preferences
2. **AI Processing** → Claude API analyzes context and recommends formula
3. **Cloud Sync** → Backend validates and stores recipe
4. **BLE Transmission** → Encrypted formula sent to ESP32 via Bluetooth
5. **Hardware Execution** → ESP32 controls pumps with PWM signals
6. **Precision Mixing** → Micro-pumps dispense exact volumes into chamber
7. **Ultrasonic Blending** → 40kHz transducer homogenizes the mixture
8. **Atomization** → Piezo atomizer creates fine mist (1-5 μm droplets)
9. **Feedback Loop** → User rating sent back for ML model improvement

### Data Models

#### User Schema (PostgreSQL)
```typescript
interface User {
  id: string;
  email: string;
  name: string;
  preferences: {
    favoriteScents: string[];
    moodProfiles: MoodProfile[];
    allergies: string[];
  };
  deviceIds: string[];
  subscriptionTier: 'free' | 'premium' | 'enterprise';
  createdAt: Date;
  lastActiveAt: Date;
}
```

#### Formula Schema
```typescript
interface Formula {
  id: string;
  userId: string;
  name: string;
  composition: {
    cartridgeId: string;
    percentage: number; // 0-100
  }[];
  metadata: {
    mood: string;
    occasion: string;
    season: string;
  };
  ratings: {
    userId: string;
    score: number; // 1-5
    timestamp: Date;
  }[];
  usageCount: number;
  isPublic: boolean;
  createdAt: Date;
}
```

#### Device State (Redis Cache)
```typescript
interface DeviceState {
  deviceId: string;
  batteryLevel: number;
  cartridges: {
    slotId: number;
    rfidUid: string;
    fragranceType: string;
    levelPercentage: number;
    lastRefilled: Date;
  }[];
  lastSync: Date;
  firmwareVersion: string;
  isOnline: boolean;
}
```

---

## 🚀 Getting Started

### Prerequisites

```bash
# Node.js 18+ and npm
node --version  # v18.x.x or higher
npm --version   # v9.x.x or higher

# React Native CLI
npm install -g react-native-cli

# iOS development (macOS only)
xcode-select --install
sudo gem install cocoapods

# Android development
# Install Android Studio and Android SDK
```

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/aira-tech/smart-perfume.git
cd smart-perfume
```

2. **Install dependencies**
```bash
# Mobile app
cd mobile-app
npm install
cd ios && pod install && cd ..

# Backend
cd ../backend
npm install

# Firmware (optional - for hardware developers)
cd ../firmware
# Use PlatformIO or Arduino IDE
```

3. **Environment configuration**
```bash
# Mobile app
cp .env.example .env
# Edit .env and add:
# - ANTHROPIC_API_KEY=your_claude_api_key
# - BACKEND_URL=http://localhost:3000

# Backend
cp .env.example .env
# Edit .env and add:
# - DATABASE_URL=postgresql://user:pass@localhost:5432/aira
# - REDIS_URL=redis://localhost:6379
# - ANTHROPIC_API_KEY=your_claude_api_key
# - JWT_SECRET=your_secret_key
```

4. **Database setup**
```bash
cd backend
npx prisma migrate dev
npx prisma db seed
```

5. **Run the application**
```bash
# Backend (Terminal 1)
cd backend
npm run dev

# Mobile app - iOS (Terminal 2)
cd mobile-app
npm run ios

# Mobile app - Android (Terminal 3)
cd mobile-app
npm run android
```

---

## 📱 Mobile App Features Deep Dive

### AI Recommendation Engine

The app integrates with **Claude API (Sonnet 4)** to provide intelligent fragrance recommendations:

```typescript
// Example: AI recommendation flow
async function getAIRecommendation(context: UserContext): Promise<Formula> {
  const prompt = `
    User Context:
    - Mood: ${context.mood}
    - Time: ${context.time}
    - Weather: ${context.weather}
    - Location: ${context.location}
    - Activity: ${context.activity}
    
    Available fragrances: ${context.availableFragrances.join(', ')}
    
    Based on this context, recommend the perfect fragrance blend.
    Return a JSON object with percentages for each fragrance.
  `;
  
  const response = await anthropic.messages.create({
    model: "claude-sonnet-4-20250514",
    max_tokens: 1000,
    messages: [{ role: "user", content: prompt }]
  });
  
  return parseFormulaFromAI(response.content);
}
```

### Real-time Device Communication

The app uses **BLE 5.0** for low-latency communication with the smart bottle:

```typescript
// Bluetooth command structure
interface BLECommand {
  type: 'DISPENSE' | 'STATUS' | 'CONFIG' | 'OTA';
  payload: {
    formula?: {
      cartridges: { id: number; volume: number }[];
    };
    config?: {
      autoMode: boolean;
      intensity: number;
    };
  };
  timestamp: number;
  checksum: string;
}

// Send formula to device
async function dispenseFormula(formula: Formula) {
  const command: BLECommand = {
    type: 'DISPENSE',
    payload: { formula: convertFormulaToHardwareFormat(formula) },
    timestamp: Date.now(),
    checksum: calculateChecksum(formula)
  };
  
  await BleManager.write(
    deviceId,
    SERVICE_UUID,
    CHARACTERISTIC_UUID,
    encrypt(JSON.stringify(command))
  );
}
```

---

## 🔧 Hardware Integration

### ESP32 Firmware Architecture

```cpp
// Main control loop
void loop() {
  // 1. Read sensor data
  float temp = dht.readTemperature();
  float humidity = dht.readHumidity();
  int batteryLevel = analogRead(BATTERY_PIN);
  
  // 2. Check for BLE commands
  if (bleCommandReceived) {
    FormulaCommand cmd = parseCommand(bleBuffer);
    executeFormula(cmd);
  }
  
  // 3. Update cartridge levels
  for (int i = 0; i < 12; i++) {
    cartridgeLevels[i] = readCapacitiveSensor(i);
  }
  
  // 4. Publish status via MQTT
  publishStatus(temp, humidity, batteryLevel, cartridgeLevels);
  
  delay(100);
}

// Precision dispensing control
void executeFormula(FormulaCommand cmd) {
  // 1. Verify RFID authentication
  for (auto& cartridge : cmd.cartridges) {
    if (!verifyRFID(cartridge.slot)) {
      sendError("COUNTERFEIT_CARTRIDGE");
      return;
    }
  }
  
  // 2. Calculate pump timings (flow rate = 5 ml/min)
  for (auto& cartridge : cmd.cartridges) {
    float volumeML = cartridge.percentage / 100.0 * TOTAL_VOLUME;
    int pumpTimeMs = (volumeML / 5.0) * 60000; // Convert to milliseconds
    
    // 3. Activate pump with PWM
    ledcWrite(PUMP_CHANNEL[cartridge.slot], 255); // Full speed
    delay(pumpTimeMs);
    ledcWrite(PUMP_CHANNEL[cartridge.slot], 0);   // Stop
  }
  
  // 4. Activate ultrasonic mixer
  digitalWrite(ULTRASONIC_PIN, HIGH);
  delay(2500); // 2.5 seconds mixing
  digitalWrite(ULTRASONIC_PIN, LOW);
  
  // 5. Ready for spray
  sendStatus("READY_TO_SPRAY");
}
```

### Pump Calibration

Each micro-pump is calibrated for precise dispensing:

```cpp
// Calibration routine (run once per cartridge)
void calibratePump(int pumpId) {
  const int TEST_RUNS = 10;
  const float TARGET_VOLUME = 1.0; // ml
  
  float avgVolume = 0;
  for (int i = 0; i < TEST_RUNS; i++) {
    float dispensed = dispensePump(pumpId, TARGET_VOLUME);
    avgVolume += dispensed;
    delay(1000);
  }
  avgVolume /= TEST_RUNS;
  
  // Calculate correction factor
  float correctionFactor = TARGET_VOLUME / avgVolume;
  EEPROM.write(CALIBRATION_ADDR + pumpId, correctionFactor * 100);
  EEPROM.commit();
}
```

---

## 🧪 Testing

### Mobile App Tests

```bash
# Unit tests
cd mobile-app
npm run test

# E2E tests (Detox)
npm run test:e2e:ios
npm run test:e2e:android

# Component tests (Storybook)
npm run storybook
```

### Backend Tests

```bash
cd backend
npm run test           # Unit tests (Jest)
npm run test:integration  # Integration tests
npm run test:load      # Load testing (k6)
```

### Hardware Tests

```bash
cd firmware
pio test  # PlatformIO unit tests

# Manual testing checklist:
# ✓ RFID authentication
# ✓ Pump precision (±0.05ml)
# ✓ Mixing homogeneity
# ✓ Battery life (300+ sprays)
# ✓ BLE connection stability
# ✓ Sensor accuracy
```

---

## 📊 Future Roadmap

### Phase 1: MVP Development (Q2 2026)
- [x] Hardware prototype design (7 technical figures completed)
- [x] Patent application filed (SAIP)
- [x] Mobile app UI/UX design (5 screens)
- [ ] Functional prototype assembly
- [ ] Basic AI recommendation engine
- [ ] Beta testing with 50 users

### Phase 2: Production Ready (Q3 2026)
- [ ] Manufacturing partner selection
- [ ] Cartridge supply chain setup
- [ ] Cloud infrastructure deployment (AWS)
- [ ] Advanced ML models for personalization
- [ ] App Store & Google Play submission
- [ ] Regulatory certifications (CE, FCC, SFDA)

### Phase 3: Market Launch (Q4 2026)
- [ ] Limited edition launch (1,000 units)
- [ ] Influencer partnerships
- [ ] Retail distribution (luxury boutiques)
- [ ] Subscription model for cartridge refills
- [ ] Customer support infrastructure

### Phase 4: Scale & Expansion (2027)
- [ ] International markets (UAE, USA, Europe)
- [ ] B2B partnerships (hotels, spas, airlines)
- [ ] Aromatherapy features (therapeutic blends)
- [ ] Voice assistant integration (Alexa, Google Home)
- [ ] AR try-before-you-buy feature
- [ ] Community marketplace for sharing recipes

### Long-term Vision (2028+)
- [ ] Medical applications (stress reduction, sleep improvement)
- [ ] Seasonal limited edition cartridges
- [ ] Celebrity fragrance collaborations
- [ ] Smart home ecosystem integration
- [ ] Biodegradable cartridges
- [ ] AI-generated signature scents

---

## 🤝 Contributing

We welcome contributions from developers, designers, and fragrance enthusiasts!

### Development Workflow

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Code Standards

- **TypeScript**: Strict mode enabled
- **Linting**: ESLint + Prettier
- **Commit messages**: Conventional Commits format
- **Testing**: Minimum 80% code coverage
- **Documentation**: JSDoc for all public APIs

---

## 📄 License

**Proprietary License** - Patent Pending (Saudi Authority for Intellectual Property)

This project is protected intellectual property. Unauthorized copying, modification, distribution, or commercial use is strictly prohibited. For licensing inquiries, contact: [legal@aira-tech.com](mailto:legal@aira-tech.com)

---

## 👥 Team

**Aira Tech Smart Fragrances LLC**

- **Saqr Al-Qahtani** - CEO & Founder
- **Nayef Al-Harbi** - CTO (Technical Architecture & Hardware Design)
- **Ziyad Al-Shammari** - Chief Perfumer (Fragrance Chemistry)
- **Noura Al-Mansour** - CMO (Marketing & Business Development)

---

## 📞 Contact

- **Website**: [www.aira-perfume.com](https://www.aira-perfume.com)
- **Email**: [info@aira-tech.com](mailto:info@aira-tech.com)
- **LinkedIn**: [Aira Tech](https://linkedin.com/company/aira-tech)
- **Twitter**: [@AiraPerfume](https://twitter.com/AiraPerfume)
- **Support**: [support@aira-tech.com](mailto:support@aira-tech.com)

---

## 🙏 Acknowledgments

- **Anthropic** - Claude API for AI-powered recommendations
- **React Native Community** - Mobile framework
- **ESP32 Community** - Embedded systems support
- **Saudi Authority for IP** - Patent filing assistance
- **Monshaat** - Startup ecosystem support

---

<p align="center">
  <img src="docs/images/logo-gold.png" alt="Aira Logo" width="200"/>
</p>

<p align="center">
  <strong>Crafting the Future of Fragrance, One Molecule at a Time</strong>
</p>

<p align="center">
  Made with ❤️ in Riyadh, Saudi Arabia 🇸🇦
</p>
