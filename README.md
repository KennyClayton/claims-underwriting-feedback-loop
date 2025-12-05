# Underwriting Insights System

## Mission Statement

A property insurance system that creates a feedback loop between claims data and underwriting decisions, enabling data-driven risk assessment and reducing loss ratios through intelligent risk scoring.

### Personal Growth

📚 My Knowledge Gaps in the Underwriting Domain:

  ✅ I understand claims (strength)
  
  ⚠️ Gap: Underwriting guidelines and appetites (what makes a risk acceptable vs. not)
  
  ⚠️ Gap: Rating engines and premium calculation formulas
  
  ⚠️ Gap: Reinsurance concepts (how companies offload risk)


Technologies:

  ✅ I'm brushing  up on SQL and .NET
  
  ✅ I have three years of exposure to Guidewire as a user (ClaimCenter and PolicyCenter)
  
  ⚠️ Gap: Policy administration systems (Duck Creek, Guidewire, Insurity)
  
  ⚠️ Gap: Limited exposure to API integrations (how systems talk to each other)
  
  ⚠️ Gap: Data warehousing concepts (where historical data lives)


Business/Systems Analyst Skills:

  ✅ Currently doing requirements gathering (this project!)
  
  ✅ Currently creating diagrams and documentation
  
  ⚠️ Gap: Writing formal BRDs (Business Requirements Documents)
  
  ⚠️ Gap: Process flow mapping (BPMN diagrams)
  
  ⚠️ Gap: UAT (User Acceptance Testing) planning


  What I'm learning NOW in this project is valuable to employers.

## Problem Statement

Current property insurance systems operate with underwriting and claims departments in silos. Underwriters make risk decisions based on static guidelines and limited historical context, while valuable claims data that could inform better underwriting decisions remains isolated in separate systems. This disconnect leads to:

- Inconsistent risk assessment
- Missed warning signs on high-risk properties
- No feedback mechanism to learn from past underwriting decisions
- Higher-than-necessary loss ratios
- Reactive rather than proactive risk management

## Solution Overview

The Underwriting Insights System bridges the gap between claims history and underwriting decisions by:

1. **Real-Time Risk Scoring** - Automatically calculating risk scores based on property characteristics and historical claims data
2. **Intelligent Alerts** - Flagging high-risk indicators during the quote process
3. **Data-Driven Dashboards** - Providing underwriters with claims history for similar properties
4. **Feedback Loop** - Feeding claims data back into the risk model to continuously improve accuracy
5. **Performance Tracking** - Measuring underwriting decision quality against actual claim outcomes

## System Architecture

### Use Case Diagrams

**Current State:** Disconnected systems where underwriting and claims operate independently

**Future State:** Integrated system with real-time risk scoring engine connecting all stakeholders

### Entity Relationship Diagram (ERD)

The system tracks relationships between:
- Customers and their properties
- Properties and their insurance policies
- Policies and their risk scores
- Claims and the risk factors they identify
- Historical patterns that inform future decisions

**Core Entities:**
- Customer
- Property
- Policy
- Claim
- Risk Score
- Risk Factor
- Underwriter
- Agent

### Object Diagram
<img width="4546" height="1310" alt="Object Diagram - Claims-UW-Feedback-Loop" src="https://github.com/user-attachments/assets/6ae8a7ca-80db-4999-9d40-0b8194f99a68" />

### Technology Stack

- **Backend:** .NET Core 8.0 / C#
- **Database:** SQL Server
- **ORM:** Entity Framework Core
- **API:** RESTful Web API
- **Architecture:** Clean Architecture with separation of concerns

## Key Features

### For Insurance Agents
- Submit applications with instant risk feedback
- View real-time risk scores and alerts
- Generate risk-adjusted quotes automatically

### For Underwriters
- Access comprehensive risk dashboards
- Review claims history for similar properties
- Make data-driven approval decisions
- Track underwriting performance metrics

### For Claims Adjusters
- Record claims that automatically feed into risk scoring
- Identify risk factors during claim processing

### Risk Scoring Engine
- Analyzes property characteristics (roof age, construction type, location)
- Incorporates historical claims patterns
- Calculates predicted loss ratios
- Provides risk level classifications (Low, Medium, High)

## Project Structure

```
UnderwritingInsights/
├── src/
│   ├── UnderwritingInsights.API/          # Web API Layer
│   ├── UnderwritingInsights.Application/  # Business Logic
│   ├── UnderwritingInsights.Domain/       # Domain Models
│   └── UnderwritingInsights.Infrastructure/ # Data Access
├── database/
│   ├── schema.sql                         # Database schema
│   └── seed-data.sql                      # Sample data
├── docs/
│   ├── use-case-current.md
│   ├── use-case-proposed.md
│   ├── erd.md
│   └── object-diagram.md
└── README.md
```

## Getting Started

### Prerequisites
- .NET 8.0 SDK
- SQL Server 2019 or later
- Visual Studio 2022 or VS Code

### Installation

1. Clone the repository
```bash
git clone https://github.com/[your-username]/underwriting-insights.git
cd underwriting-insights
```

2. Set up the database
```bash
# Execute schema.sql in SQL Server Management Studio
# Then execute seed-data.sql for sample data
```

3. Update connection string in appsettings.json

4. Run the application
```bash
dotnet run --project src/UnderwritingInsights.API
```

## Future Enhancements

- Machine learning models for advanced risk prediction
- Integration with third-party data sources (weather, crime statistics)
- Mobile app for agents
- Advanced analytics and reporting dashboards
- Automated policy renewal risk assessment

## About This Project

This project demonstrates systems analysis and development skills including:
- Business process analysis and improvement
- Database design and normalization
- Object-oriented programming with C#
- RESTful API development
- Entity Framework Core and LINQ
- Clean architecture principles

Built as a portfolio demonstration of bridging insurance domain knowledge with technical development capabilities.

## Contact

Kenny Clayton

[LinkedIn](https://www.linkedin.com/in/kenny-clayton/)

---

*This system demonstrates how technology can transform insurance operations by connecting previously siloed data to enable smarter, data-driven decisions.*
