# Underwriting Insights System

## Mission Statement

A property insurance system that creates a feedback loop between claims data and underwriting decisions, enabling data-driven risk assessment and reducing loss ratios through intelligent risk scoring.

## 📚 Documentation Hub

- **[Confluence Space](https://insuranceanalystportfolio.atlassian.net/wiki/spaces/~7120205585746639fc495e9b332e6647573f67/pages/edit-v2/3801089?draftShareId=fcb0d80b-220e-4f31-8925-9f87c4d65411)** - Full system documentation
- **[System Glossary](./docs/glossary.md)** - Complete definitions and scoring methodology
- **[Risk Scoring Guide](./docs/risk-scoring-methodology.md)** - Detailed calculation methods
- **[Jira Board](#)** - Project tracking (coming soon)

---

## 🎯 Personal Growth Journey

### My Knowledge Gaps in the Underwriting Domain:

✅ **Strengths:**
- Deep understanding of property claims processes
- 3 years exposure to Guidewire as a User (ClaimCenter and PolicyCenter)
- Currently learning SQL and .NET Core
- Requirements gathering and documentation

⚠️ **Learning Through This Project:**
- Underwriting guidelines and risk appetites
- Rating engines and premium calculation formulas
- Reinsurance concepts (how companies offload risk)
- Policy administration system integrations
- API design and implementation
- Data warehousing concepts
- Writing formal Business Requirements Documents (BRDs)
- Process flow mapping (BPMN diagrams)
- User Acceptance Testing (UAT) planning

**What I'm learning NOW in this project is directly applicable to Business/Systems Analyst roles in insurance.**

---

## Problem Statement

Current property insurance systems operate with underwriting and claims departments in silos. Underwriters make risk decisions based on static guidelines and limited historical context, while valuable claims data that could inform better underwriting decisions remains isolated in separate systems. This disconnect leads to:

- Inconsistent risk assessment
- Missed warning signs on high-risk properties
- No feedback mechanism to learn from past underwriting decisions
- Higher-than-necessary loss ratios
- Reactive rather than proactive risk management
- Limited visibility into property-level claim history across insurers

## Solution Overview

The Underwriting Insights System bridges the gap between claims history and underwriting decisions by:

1. **Real-Time Risk Scoring** - Automatically calculating risk scores (0-100 scale) based on property characteristics and historical claims data
2. **Intelligent Alerts** - Flagging high-risk indicators during the quote process
3. **Data-Driven Dashboards** - Providing underwriters with claims history for similar properties
4. **Feedback Loop** - Feeding claims data back into the risk model to continuously improve accuracy
5. **Performance Tracking** - Measuring underwriting decision quality against actual claim outcomes
6. **Premium Surcharge Logic** - Offering pricing alternatives instead of outright declines for elevated risks
7. **Prior Claims Intelligence** - Leveraging Florida 626 requests to access property-level claim history across carriers
8. **Catastrophe Event Tracking** - Identifying and analyzing claims from major weather events (hurricanes, tornadoes, hail storms)

---

## System Architecture

### Use Case Diagrams

**Current State:** Disconnected systems where underwriting and claims operate independently

**Future State:** Integrated system with real-time risk scoring engine connecting all stakeholders

📊 [View detailed use case diagrams in Confluence](#)

### Entity Relationship Diagram (ERD)

The system tracks relationships between:
- Customers and their properties
- Properties and their insurance policies
- Policies and their risk scores
- Claims and the risk factors they identify
- Historical patterns that inform future decisions
- **NEW:** Prior claim history via FL 626 requests
- **NEW:** Catastrophe event associations

**Core Entities:**
- Customer
- Property
- Policy
- Claim (with catastrophe subtypes)
- Risk Score
- Risk Factor
- Underwriter
- Agent
- **PriorClaimsRequest** (FL 626 tracking)
- **UnderwritingDecision** (approve, surcharge, decline)

📊 [View full ERD in Confluence](#)

### Object Diagram
<img width="4546" height="1310" alt="Object Diagram - Claims-UW-Feedback-Loop" src="https://github.com/user-attachments/assets/6ae8a7ca-80db-4999-9d40-0b8194f99a68" />

### Technology Stack

- **Backend:** .NET Core 8.0 / C#
- **Database:** SQL Server 2019+
- **ORM:** Entity Framework Core
- **API:** RESTful Web API
- **Architecture:** Clean Architecture with separation of concerns
- **Documentation:** Confluence + Jira
- **Version Control:** Git/GitHub

---

## Key Features

### For Insurance Agents
- Submit applications with instant risk feedback
- View real-time risk scores (0-100 scale with color coding)
- Generate risk-adjusted quotes automatically
- See alerts for high-risk property characteristics
- Access prior claim history for properties

### For Underwriters
- Access comprehensive risk dashboards
- Review claims history for similar properties (based on location, age, construction)
- Make data-driven approval decisions with multiple options:
  - **Approve Standard** (Low risk: 0-35)
  - **Approve with Surcharge** (Medium-High risk: 65-85)
  - **Decline** (High risk: 85-100 or unacceptable factors)
  - **Refer to Senior UW** (Complex cases)
- Track underwriting performance metrics
- View predicted loss ratios before binding
- Initiate FL 626 prior claims requests
- Analyze catastrophe event impacts

### For Claims Adjusters
- Record claims that automatically feed into risk scoring
- Identify and tag risk factors during claim processing
- Flag catastrophe events (hurricanes, tornadoes, hail, wind)
- Link claims to NOAA-declared weather events

### Risk Scoring Engine
- Analyzes 20+ property characteristics:
  - **Physical:** Roof age/type, construction type, year built, square footage
  - **Location:** Coastal proximity, flood zone, fire district rating, wildfire risk
  - **Occupancy:** Primary/secondary/rental, vacancy duration, security features
  - **Historical:** Prior claim count, maintenance history, FL 626 findings
- Incorporates historical claims patterns from similar properties
- Calculates predicted loss ratios (% of premium expected in claims)
- Provides risk level classifications:
  - 🟢 **Low Risk** (0-35): Standard approval
  - 🟡 **Medium Risk** (36-65): Manual review, possible surcharge
  - 🔴 **High Risk** (66-100): Senior review, surcharge, or decline
- Handles catastrophe events separately (hail, hurricane, tornado, wind)

---

## Key Business Logic

### Property Similarity Matching
Properties are considered "similar" when they match on:
- Geographic region (same state + coastal/inland designation)
- Property age bracket (within 10-year bands)
- Roof age category (<5, 5-10, 10-15, 15-20, 20+ years)
- Construction type (frame, masonry, etc.)
- Coverage amount band (within 25%)

### Premium Surcharge Decision Logic
When risk score is elevated but not unacceptable:
- **Score 36-65 (Medium):** 0-15% surcharge
- **Score 66-85 (Medium-High):** 15-30% surcharge
- **Predicted Loss Ratio 70-85%:** 20-40% surcharge
- **Score 85-100 (High):** Decline or 30%+ surcharge with conditions

### Florida 626 Prior Claims Integration
- Automatically triggers for properties with prior loss indicators
- Requests claim history from previous carriers (same property address)
- Feeds historical claims into risk scoring
- Compliance: Adheres to FL Statute 626.9541 requirements
- **Risk Impact:** Prior claims at same property location carry high weight (8-10) in scoring

### Catastrophe Event Handling
- Claims flagged as catastrophe type (HAIL, HURRICANE, TORNADO, WIND_NON_HURRICANE)
- Linked to NOAA event declarations
- Analyzed separately in risk models (not penalized as heavily as individual incidents)
- Used to identify geographic risk patterns

---

## Project Structure

```
claims-underwriting-feedback-loop/
├── src/
│   ├── UnderwritingInsights.API/          # Web API Layer
│   ├── UnderwritingInsights.Application/  # Business Logic
│   ├── UnderwritingInsights.Domain/       # Domain Models
│   └── UnderwritingInsights.Infrastructure/ # Data Access & EF Core
├── database/
│   ├── 01-create-schema.sql              # Database schema
│   ├── 02-create-tables.sql              # Table definitions
│   ├── 03-create-indexes.sql             # Performance indexes
│   ├── 04-create-stored-procedures.sql   # SP for risk calculations
│   └── 05-seed-data.sql                  # Sample test data
├── docs/
│   ├── glossary.md                       # System glossary & definitions
│   ├── risk-scoring-methodology.md       # Detailed scoring algorithms
│   ├── use-cases.md                      # Use case documentation
│   ├── fl-626-integration.md             # Prior claims request process
│   └── catastrophe-handling.md           # CAT event logic
├── diagrams/
│   ├── current-state-use-case.png
│   ├── future-state-use-case.png
│   ├── erd.png
│   └── object-diagram.png
├── tests/
│   ├── UnderwritingInsights.UnitTests/
│   └── UnderwritingInsights.IntegrationTests/
└── README.md
```

---

## Getting Started

### Prerequisites
- .NET 8.0 SDK ([Download](https://dotnet.microsoft.com/download))
- SQL Server 2019 or later ([Download SQL Server Express](https://www.microsoft.com/en-us/sql-server/sql-server-downloads))
- Visual Studio 2022 or VS Code
- Git

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/KennyClayton/claims-underwriting-feedback-loop.git
cd claims-underwriting-feedback-loop
```

2. **Set up the database**
```bash
# Open SQL Server Management Studio (SSMS)
# Connect to your SQL Server instance
# Execute scripts in order:
# 1. database/01-create-schema.sql
# 2. database/02-create-tables.sql
# 3. database/03-create-indexes.sql
# 4. database/04-create-stored-procedures.sql
# 5. database/05-seed-data.sql
```

3. **Configure the application**
```bash
# Update src/UnderwritingInsights.API/appsettings.json
# Set your SQL Server connection string:
"ConnectionStrings": {
  "DefaultConnection": "Server=localhost;Database=UnderwritingInsights;Trusted_Connection=True;"
}
```

4. **Run the application**
```bash
cd src/UnderwritingInsights.API
dotnet restore
dotnet build
dotnet run
```

5. **Access the API**
- API will be running at: `https://localhost:5001`
- Swagger documentation: `https://localhost:5001/swagger`

---

## Risk Scoring Quick Reference

| Score Range | Risk Level | Color | Action |
|-------------|------------|-------|--------|
| 0-35 | Low | 🟢 Green | Standard approval |
| 36-65 | Medium | 🟡 Yellow | Manual review, possible surcharge |
| 66-85 | Medium-High | 🟠 Orange | Senior review, surcharge likely |
| 86-100 | High | 🔴 Red | Decline or significant surcharge |

**Predicted Loss Ratio Interpretation:**
- 0-50%: Highly profitable
- 51-70%: Target range for profitability
- 71-90%: Needs premium adjustment
- 91-100%+: Decline or require significant risk improvements

📖 [Full glossary and methodology documentation](./docs/glossary.md)

---

## Development Roadmap

### Phase 1: System Analysis & Design ✅
- [x] Create use case diagrams
- [x] Design database ERD
- [x] Document system glossary
- [x] Define risk scoring methodology

### Phase 2: Database Development 🔄 (In Progress)
- [ ] Create database schema
- [ ] Build stored procedures for risk calculations
- [ ] Implement seed data with realistic scenarios
- [ ] Add indexes for performance

### Phase 3: Core Domain Models
- [ ] Implement entity classes (Customer, Property, Policy, Claim, etc.)
- [ ] Set up Entity Framework Core
- [ ] Create data repositories
- [ ] Build domain services

### Phase 4: Risk Scoring Engine
- [ ] Build risk factor calculator
- [ ] Implement property similarity matching algorithm
- [ ] Create scoring algorithm with weighted factors
- [ ] Build predicted loss ratio model
- [ ] Integrate FL 626 prior claims data

### Phase 5: API Development
- [ ] Create Policy endpoints (CRUD operations)
- [ ] Create Risk Score calculation endpoints
- [ ] Create Claims endpoints
- [ ] Build Underwriter dashboard API
- [ ] Implement catastrophe event queries

### Phase 6: Testing & Documentation
- [ ] Write unit tests (80%+ coverage goal)
- [ ] Integration testing
- [ ] API documentation (Swagger)
- [ ] User guide
- [ ] Deployment guide

---

## Future Enhancements

- 🤖 Machine learning models for advanced risk prediction
- 🌦️ Integration with third-party data sources (NOAA weather, crime statistics, ISO ratings)
- 📱 Mobile app for agents
- 📊 Advanced analytics and reporting dashboards
- 🔄 Automated policy renewal risk assessment
- 🗺️ Geographic risk heat maps
- 📧 Automated underwriter alerts and workflows
- 🔗 Integration with policy administration systems (Guidewire, Duck Creek)

---

## Learning Resources

This project involves multiple technologies and concepts. Here are resources I'm using:

**SQL & Database Design:**
- [Microsoft SQL Server Documentation](https://docs.microsoft.com/en-us/sql/sql-server/)
- Database normalization principles

**.NET Core & C#:**
- [Microsoft .NET Documentation](https://docs.microsoft.com/en-us/dotnet/)
- [Entity Framework Core Documentation](https://docs.microsoft.com/en-us/ef/core/)

**Insurance Domain Knowledge:**
- Underwriting guidelines and risk assessment
- Property insurance claim patterns
- Florida insurance regulations (626.9541)

**Systems Analysis:**
- Use case diagrams (UML)
- Entity-Relationship Diagrams
- Business process modeling

---

## About This Project

This project demonstrates systems analysis and development skills including:
- ✅ Business process analysis and improvement
- ✅ Requirements gathering and documentation
- ✅ Database design and normalization
- ✅ Object-oriented programming with C#
- ✅ RESTful API development
- ✅ Entity Framework Core and LINQ
- ✅ Clean architecture principles
- ✅ Insurance domain knowledge (claims + underwriting)
- ✅ Jira/Confluence documentation practices

**Built as a portfolio demonstration** of bridging insurance domain knowledge with technical development capabilities for Business Analyst and Systems Analyst roles.

---

## Project Status

**Current Phase:** Phase 2 - Database Development  
**Last Updated:** December 2024  
**Completion:** ~20% (System design complete, beginning implementation)

---

## Contact

**Kenny Clayton**  
Systems Analyst | Insurance Technology  
[LinkedIn](https://www.linkedin.com/in/kenny-clayton/)  
[GitHub](https://github.com/KennyClayton)

---

## License

This is a portfolio/educational project. Feel free to reference the architecture and concepts for learning purposes.

---

*This system demonstrates how technology can transform insurance operations by connecting previously siloed data to enable smarter, data-driven decisions. By bridging claims experience with underwriting intelligence, we can reduce loss ratios while improving risk selection.*
