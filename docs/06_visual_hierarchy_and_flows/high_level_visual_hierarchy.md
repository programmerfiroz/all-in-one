# HIGH-LEVEL VISUAL HIERARCHY & SYSTEM FLOW BLUEPRINT
## India-First Modular Super App Platform (All Verticals & Applications)

**Document Identifier:** VHB-IND-V1.1  
**Project Category:** Multi-Vertical Digital Super App Ecosystem  
**Target Market:** India (Tier 1, Tier 2, Tier 3, Semi-Urban)  
**Parent Documents:** Master Project Charter (MPC-IND-V1.0), Product Breakdown Structure (PBS-IND-V1.0), Business Requirements Document (BRD-IND-V1.0), Remediation Plan V1.1 (ERP-IND-V1.1)  
**Document Type:** Exhaustive Visual Architecture, Functional Hierarchy & End-to-End Operational Flow Blueprint  
**Status:** Authoritative Visual Specification (100% GitHub Markdown & Mermaid Compatible)  

---

## 1. Document Overview & Visual Architecture Scope

This document provides the complete, authoritative visual blueprint of the **India-First Modular Super App Platform**. It visually breaks down every shared foundation service, application component, vertical operational lifecycle, financial ledger movement, high-concurrency guard, and anti-fraud pipeline into structured diagrams.

All diagrams are designed to render natively on GitHub with zero syntax conflicts (no semicolons in sequence diagrams, no raw line breaks, and no unescaped arrow tokens inside labels).

---

## 2. Master System Visual Topology (6-Tier Macro Architecture)

```mermaid
graph TD
    subgraph Tier1["1. CLIENT APPLICATION SURFACES (Flutter & Next.js)"]
        App1["Customer Mobile App<br/>(iOS and Android - Flutter + BLoC)"]
        App2["Unified Workforce Mobile App<br/>(ONE Single App: Rider, Driver, Specialist)"]
        App3["Merchant Partner Mobile App<br/>(KDS, Inventory, Clinic Token, Extranet)"]
        App4["Enterprise Super Admin Web Portal<br/>(Next.js 14+ App Router / TypeScript)"]
    end

    subgraph Tier2["2. EDGE GATEWAY & SECURITY PERIMETER"]
        WAF["Cloudflare Edge WAF & DDoS Shield"]
        Kong["API Gateway & Reverse Proxy<br/>(Kong / NGINX Cluster)"]
        RateLimit["Adaptive Token Bucket Rate Limiter<br/>(Sliding Window in Redis)"]
        AuthGuard["JWT Access Token & Device Fingerprint Validator"]
    end

    subgraph Tier3["3. SHARED FOUNDATIONAL PLATFORM ENGINES"]
        IAM["Unified Indian IAM & Multi-Persona Manager<br/>(Mobile OTP, WhatsApp Fallback, RBAC)"]
        Treasury["Double-Entry Treasury Engine<br/>(64-bit Integer Paise Precision Ledger)"]
        Geo["H3 Spatial Indexing & Telemetry Hub<br/>(Uber H3 Res 7/9, Dead Reckoning)"]
        Events["Omnichannel Notification & Event Bus<br/>(FCM Priority Data Messages, DLT SMS)"]
        TaxEng["Cart, Checkout & GST Split-Invoicing Engine<br/>(Sec 9(5) vs Sec 52 Dual Invoicing)"]
        Loyalty["Universal Super Coins & Promo Subsystem<br/>(Cross-Vertical Earn and Burn)"]
        Safety["Trust, Safety & Emergency SOS Dispatcher<br/>(4-Tier Anti-Spoofing, Telemetry Anomaly)"]
        Support["Centralized Helpdesk & Dispute Arbitrator<br/>(Automated Refund Authority Matrix)"]
    end

    subgraph Tier4["4. 9 BUSINESS DOMAIN MICRO-MODULES"]
        V1["Food Delivery Vertical<br/>(Menus, KDS 15m Sync, Hot-Bag, FSSAI)"]
        V2["Grocery Delivery Vertical<br/>(Dark Stores, 10m Hold, Produce Tolerance)"]
        V3["E-Commerce Marketplace Vertical<br/>(Multi-Seller Cart, 3PL AWB, 7-Day Escrow)"]
        V4["Ride Booking & Mobility Vertical<br/>(Upfront Dynamic Fare, 4-Digit OTP, FASTag)"]
        V5["Logistics & Parcel Vertical<br/>(Hyperlocal & Inter-City, Volumetric Weight)"]
        V6["Home Services Vertical<br/>(Standard Rate Cards, In-App Extra Quotes)"]
        V7["Healthcare Services Vertical<br/>(Doctor Queue Tokens, ABDM M1-M3, Safe Harbor)"]
        V8["Education & Tutoring Vertical<br/>(Demo Classes, UPI Autopay Recurring Mandates)"]
        V9["Hotel Booking Vertical<br/>(10m Room Hold, Configurable KYC, Form C)"]
    end

    subgraph Tier5["5. PERSISTENT STORAGE, CACHE & ASYNC QUEUES"]
        DB[(PostgreSQL 16 Cluster<br/>Isolated Domain Schemas, ACID Ledger, Row Locks)]
        Redis[(Redis 7 In-Memory Cluster<br/>Lua Script Leases, Streams, Proximity GeoSets)]
        Queue["BullMQ Distributed Job Queues<br/>(Dead-Letter Workers & Outbox Recovery)"]
        S3["Object Storage<br/>(Cloudflare R2 / AWS S3 AES-256 Encrypted)"]
    end

    subgraph Tier6["6. EXTERNAL INDIAN INTEGRATIONS & REGULATORY RAILS"]
        PG["Payment Rails: Razorpay, Cashfree<br/>(UPI Intent, UPI Autopay, RuPay, NetBanking)"]
        Telecom["Telecom Rails: MSG91, Gupshup<br/>(DLT-Registered SMS, WhatsApp Business API)"]
        Maps["Geo Rails: MapmyIndia Mappls, Google Maps<br/>(Indian Landmark Parsing, Matrix Routing)"]
        Logi["3PL Logistics: Delhivery, Shiprocket<br/>(Automated Waybill Generation & Freight)"]
        Govt["Statutory APIs: GST Portal GSTR-8, BoI FRRO<br/>(GSTIN Verification, Form C Foreign Export)"]
    end

    Tier1 --> Tier2
    Tier2 --> Tier3
    Tier3 --> Tier4
    Tier4 --> Tier5
    Tier3 --> Tier6
    Tier4 --> Tier6
```

---

## 3. The 4 Client Applications: Detailed Component & Screen Topologies

---

### 3.1 Customer Mobile App (Flutter + BLoC)
```mermaid
graph TD
    subgraph CustApp["Customer Mobile App Architecture (Flutter)"]
        C_Root["Root App Shell (GetIt DI + Router)"]
        
        C_Root --> C_Auth["Auth & Onboarding Module<br/>• Mobile Number & OTP Verification<br/>• WhatsApp OTP Fallback<br/>• Language Selector (8+ Indic Languages)"]
        
        C_Root --> C_Home["Universal Discovery Feed<br/>• Geofenced Service Availability Checker<br/>• Active Order Live Tracking Floating Pill<br/>• Cross-Vertical Banner Promotions"]
        
        C_Root --> C_Verticals["Vertical Browsing Surfaces"]
        C_Verticals --> C_V1["Food & Grocery Storefront<br/>(Veg/Non-Veg Filter, Customization Drawer)"]
        C_Verticals --> C_V2["E-Commerce Catalog<br/>(Multi-Variant SKU Matrix, Pincode Delivery Check)"]
        C_Verticals --> C_V3["Ride Booking Map Surface<br/>(Vehicle Selector, Upfront Fare, Start OTP Display)"]
        C_Verticals --> C_V4["Services & Healthcare<br/>(Rate Cards, Doctor Clinic Queue, Lab Tests)"]
        C_Verticals --> C_V5["Hotels & Education<br/>(Room Hold Timer, Demo Class Slot Selector)"]
        
        C_Root --> C_Cart["Universal Cart & Checkout Engine<br/>• Multi-Seller Split Notifications<br/>• Dynamic Bill Breakdown in Paise<br/>• UPI Intent Direct App Tray (GPay, PhonePe)"]
        
        C_Root --> C_Account["Profile & Financial Hub<br/>• Closed Wallet & Super Coins Balance<br/>• Saved Addresses with Landmark Parser<br/>• Encrypted Health Locker (Prescription PDFs)<br/>• 24x7 In-App Helpdesk & Active Ticket Chat"]
    end
```

---

### 3.2 ONE Unified Workforce Mobile App (Flutter + BLoC)
Preserved strictly as **ONE single application binary** with dynamic capability gating:

```mermaid
graph TD
    subgraph WorkforceApp["ONE Unified Workforce App Architecture (Flutter)"]
        W_Auth["Unified Partner Onboarding & Document Vault<br/>• Aadhaar, PAN, Driving License, Vehicle RC Verification<br/>• Bank Penny-Drop Account Validation"]
        
        W_Auth --> W_JWT["Authenticated JWT Payload with Capabilities Array"]
        W_JWT --> W_ShellRouter{"Inspect Partner Capabilities"}
        
        W_ShellRouter -->|Contains: RIDE_DRIVER or FOOD_DELIVERY| W_TransitShell["TRANSIT & MOBILITY SHELL (Riders and Drivers)"]
        W_ShellRouter -->|Contains: TECHNICIAN or PHLEBOTOMIST| W_SpecialistShell["SPECIALIST SHELL (Home Services and Labs)"]
        W_ShellRouter -->|Qualified for Both Domains| W_DualToggle["Top App Bar Switcher: Transit Mode vs Service Mode"]
        
        subgraph TransitFeatures["Transit Shell Features"]
            W_TransitShell --> W_Radar["Floating Task Radar Card with 30s Countdown Timer"]
            W_TransitShell --> W_Shift["Shift Switcher: Delivery Mode vs Ride Mode vs Dual Mode"]
            W_TransitShell --> W_Nav["In-App Turn-by-Turn GPS Navigation with Traffic Re-routing"]
            W_TransitShell --> W_OTP["Customer Delivery & Start Ride OTP Verification Keypad"]
        end
        
        subgraph SpecialistFeatures["Specialist Shell Features"]
            W_SpecialistShell --> W_Cal["Daily Scheduled Booking Agenda & Calendar View"]
            W_SpecialistShell --> W_Quote["In-App Digital Extra Spare Parts Quotation Builder"]
            W_SpecialistShell --> W_QC["Mandatory Before and After Photo QC Uploader"]
            W_SpecialistShell --> W_Cert["30-Day Service Warranty Card Generator"]
        end
        
        subgraph SharedCore["100% Shared Foundation Services"]
            W_Common1["Daily Earnings Counter & Instant Bank Cashout via IMPS"]
            W_Common2["Native Foreground Sticky Service (Location Type)"]
            W_Common3["High-Priority Background Audio Alarm Chime Engine"]
            W_Common4["One-Touch Emergency SOS Dispatcher"]
        end
        
        W_TransitShell --> SharedCore
        W_SpecialistShell --> SharedCore
    end
```

---

### 3.3 Merchant Partner Mobile App (Flutter + BLoC)
```mermaid
graph TD
    subgraph MerchantApp["Merchant Partner Mobile App Architecture (Flutter)"]
        M_Auth["Merchant Onboarding & Digital KYC<br/>(GSTIN Auto-Fetch, FSSAI 14-Digit License Check)"]
        
        M_Auth --> M_Console{"Dynamic Business Profile Mode"}
        
        M_Console -->|Restaurant / Cloud Kitchen| M_KDS["Kitchen Display System (KDS)<br/>• Audible Chime Alert with 180s Acceptance Timer<br/>• Preparation Time Selector (15m, 25m, 40m)<br/>• Food Ready for Pickup Dispatch Trigger"]
        
        M_Console -->|Kirana / Dark Store / Retail| M_Inventory["Inventory & Catalog Manager<br/>• Instant In-Stock / Out-of-Stock Toggle<br/>• Barcode Tote Labeling for Order Pickers<br/>• Produce Weight Variance Adjuster"]
        
        M_Console -->|Clinic / Laboratory| M_Clinic["Healthcare Console<br/>• Live Digital Clinic Queue Token Management<br/>• WebRTC Teleconsultation Doctor Dashboard<br/>• Diagnostic Sample Lab Dispatch Tracker"]
        
        M_Console -->|Hotel / Property| M_Hotel["Hotelier Extranet Console<br/>• Real-Time Room Availability Calendar<br/>• Guest Digital Check-In / Check-Out Folio<br/>• BoI FRRO Form C Foreign Guest Submission Desk"]
        
        M_Console --> M_Fin["Financial Settlement Dashboard<br/>• Daily Gross Sales & Commission Deductions<br/>• Section 194-O TDS & Section 52 TCS Breakdown<br/>• Automated T+1 Net Payout Status Tracker"]
    end
```

---

### 3.4 Enterprise Super Admin Web Portal (Next.js 14+ / TypeScript)
```mermaid
graph TD
    subgraph AdminPortal["Enterprise Super Admin & Operations Portal (Next.js)"]
        A_RBAC["Granular Role-Based Access Control (RBAC)<br/>(Super Admin, City Ops Manager, KYC Officer, Finance Lead)"]
        
        A_RBAC --> A_Ops["City Operations Command Center<br/>• Live Geospatial Fleet Clusters & Telemetry Heatmap<br/>• Dynamic Surge Multiplier Activation Console<br/>• Stuck Task Reassignment & Manual Dispatch Overrides"]
        
        A_RBAC --> A_KYC["Partner Governance & Verification Vault<br/>• Merchant FSSAI & Storefront Image Verification<br/>• Driver DL, RC, Commercial Permit & Police Check<br/>• Blacklisted Account Suspension Desk"]
        
        A_RBAC --> A_GIS["GIS Zone & Polygon Editor<br/>• GeoJSON Boundary Drawer for Cities & Micro-Clusters<br/>• Uber H3 Resolution 7 and Resolution 9 Zone Config"]
        
        A_RBAC --> A_Finance["Treasury, Statutory Tax & Reconciliation Hub<br/>• Automated Gateway Clearing vs Bank Statement Reconciliation<br/>• GSTR-8 Monthly Export (0.5% GST TCS Deduction Data)<br/>• Section 194-O TDS Form 16A Certificate Dispatch<br/>• Platform Double-Entry General Ledger Balance Audit"]
    end
```

---

## 4. Clean Architecture & BLoC Reactive Event Flow (Flutter Mobile Layer)

```mermaid
sequenceDiagram
    autonumber
    actor Screen as Flutter UI Page (BlocBuilder)
    participant Bloc as FeatureBLoC (Presentation)
    participant UseCase as Domain UseCase (Business Domain)
    participant Repo as RepositoryImpl (Data Layer)
    participant LocalDB as Local Store (Hive / SQLite)
    participant RemoteAPI as Backend REST / WebSocket API

    Screen->>Bloc: User triggers action (dispatches FeatureEvent)
    Note over Bloc: BLoC emits FeatureLoadingState
    Bloc->>UseCase: Invokes execute(params)
    UseCase->>UseCase: Validate business rules and validation constraints
    UseCase->>Repo: Calls repository interface contract
    
    alt Read Pattern (Offline-First with Background Delta)
        Repo->>LocalDB: Fetch cached domain entities (zero latency)
        LocalDB-->>Repo: Return cached records
        Repo-->>UseCase: Return Either.Right(data)
        UseCase-->>Bloc: Return success payload
        Bloc-->>Screen: Emits FeatureLoadedState (Instant UI render)
        
        Repo->>RemoteAPI: Fire non-blocking HTTP/2 delta request
        RemoteAPI-->>Repo: Return delta records since timestamp
        Repo->>LocalDB: Update local persistent database
        Repo-->>Bloc: Emits FeatureDeltaUpdatedState
        Bloc-->>Screen: Silently updates UI without page flicker
    else Transactional Mutating Pattern (Order Placement / Payment)
        Repo->>RemoteAPI: POST /api/v1/resource with X-Idempotency-Key
        RemoteAPI-->>Repo: Return HTTP 200 OK + Payload
        Repo->>LocalDB: Persist transaction in local ledger table
        Repo-->>UseCase: Return Either.Right(success)
        UseCase-->>Bloc: Transaction committed
        Bloc-->>Screen: Emits FeatureSuccessState (Trigger Navigation)
    end
```

---

## 5. End-to-End Operational Workflows Across the 9 Verticals

---

### 5.1 Vertical 1: Food Delivery Operational Workflow
```mermaid
sequenceDiagram
    autonumber
    actor Cust as Customer App
    participant Core as Food Order Service
    actor Rest as Restaurant KDS
    participant Redis as Redis Lua Lease Engine
    participant DB as PostgreSQL Outbox
    actor Rider as Workforce App (Transit Mode)

    Cust->>Core: Place Food Order (UPI Intent or COD)
    Core->>Rest: Push High-Priority Audio Chime Alert to Partner App
    Rest->>Core: Kitchen Confirms Order (Sets Prep Time: 15 mins)
    
    Note over Core,Redis: Dispatcher computes Rider ETA to match Kitchen Ready Time
    Core->>Redis: Execute Atomic Lua Lease (DISPATCH_LOCK_EX30)
    Redis-->>Core: Lock Acquired (Monotonic Fencing Token: 10482)
    Core->>DB: INSERT INTO dispatch_assignments (status: 'OFFERED', expires_at: NOW()+30s)
    
    Core->>Rider: Push Task Offer Card (30-second Acceptance Timer)
    Rider->>Core: Rider Accepts Task
    Core->>DB: UPDATE dispatch_assignments SET status = 'CONFIRMED'
    Core->>Redis: SET driver:state:DRV_101 "ENGAGED"
    
    Rider->>Rest: Arrives at restaurant, verifies Order ID, checks hot-bag seal
    Rest->>Rider: Hands over packaged meal with tamper-evident seal
    Rider->>Cust: In transit to delivery address (Live telemetry tracking)
    
    Rider->>Cust: Arrives at doorstep, requests Delivery OTP
    Cust->>Rider: Customer shares 4-digit OTP
    Rider->>Core: Submit Delivery OTP
    Core->>Core: Order marked DELIVERED and release merchant and rider ledger credits
```

---

### 5.2 Vertical 2: Grocery Delivery (Dark Store & Kirana) Workflow
```mermaid
flowchart TD
    Browse["Customer adds Grocery items to Cart"] --> ReserveHold["10-Minute Pessimistic Stock Reservation Lock on Inventory"]
    ReserveHold --> Checkout["Customer Completes Checkout via UPI"]
    
    RouteStore["Order routed to Nearest Dark Store / Partner Kirana"]
    Checkout --> RouteStore
    RouteStore --> Picker["Store Picker App displays route-optimized item picking list"]
    
    Picker --> ScanBarcode["Picker scans barcode of each item into tote"]
    
    ScanBarcode --> ItemCheck{"Are all items in stock?"}
    
    ItemCheck -->|Yes All In Stock| PackBag["Pack items in eco-friendly tote, seal bag with barcode"]
    
    ItemCheck -->|Item Missing Out of Stock| SubEngine{"Evaluate Customer Substitution Rule"}
    SubEngine -->|Rule A: Auto-Substitute| ReplaceItem["Substitute with closest premium brand item"]
    SubEngine -->|Rule B: Contact Customer| PhoneCall["Trigger automated phone call alert to customer"]
    SubEngine -->|Rule C: Drop and Refund| DropItem["Drop item, auto-refund item cost to Customer Wallet"]
    
    ReplaceItem --> PackBag
    PhoneCall --> PackBag
    DropItem --> PackBag
    
    PackBag --> FreshCheck{"Contains Fresh Produce by Weight?"}
    FreshCheck -->|Yes Produce Included| WeighScale["Weigh produce on digital scale (±10% tolerance)"]
    WeighScale --> DeltaCalc["If weight is lower, auto-refund exact delta in Paise to Wallet"]
    DeltaCalc --> DispatchFleet["Assign Last-Mile Delivery Partner"]
    FreshCheck -->|No Standard Packaged| DispatchFleet
    
    DispatchFleet --> Delivery["Doorstep Delivery with 4-Digit Customer OTP Verification"]
```

---

### 5.3 Vertical 3: E-Commerce Marketplace Workflow
```mermaid
flowchart TD
    MultiCart["Customer adds items from Seller A and Seller B to Cart"] --> Pay["Single Unified Payment via UPI / Card"]
    Pay --> SplitOrders["Backend splits Master Order into Sub-Orders: SubOrder_A and SubOrder_B"]
    
    SplitOrders --> PackA["Seller A packs item and prints automated 3PL Shipping Label and Manifest"]
    SplitOrders --> PackB["Seller B packs item and prints automated 3PL Shipping Label and Manifest"]
    
    PackA --> CourierA["Delhivery Courier picks up package from Seller A warehouse"]
    PackB --> CourierB["Shiprocket Courier picks up package from Seller B warehouse"]
    
    CourierA --> HubSort["Regional Sorting Hub and Inter-City Line-Haul Transit"]
    CourierB --> HubSort
    
    HubSort --> DestinationHub["Destination City Hub and Out for Delivery Assignment"]
    DestinationHub --> Doorstep["Courier arrives at Customer Doorstep"]
    Doorstep --> InspectDel["Customer inspects outer package and shares Delivery OTP"]
    
    InspectDel --> CoolingWindow["7-Day Statutory Return and Replacement Cooling Window"]
    
    CoolingWindow -->|No Return Initiated| EscrowRelease["7-Day Escrow Expires: Platform releases payout to Seller bank account"]
    CoolingWindow -->|Customer Requests Return| ReverseQC["Doorstep Reverse Pickup scheduled with physical QC inspection"]
```

---

### 5.4 Vertical 4: Ride Booking & Mobility Workflow
```mermaid
sequenceDiagram
    autonumber
    actor Rider as Customer App
    participant Back as Mobility Backend
    actor Driver as Workforce App (Ride Mode)

    Rider->>Back: Select Destination and Request Ride Fare
    Back->>Rider: Display Guaranteed Upfront Fare (Tolls and Surge capped per MV Rules)
    Rider->>Back: Confirm Booking (Issue 4-Digit Start OTP)
    
    Back->>Driver: Geo-spatial Proximity Broadcast to nearest available drivers
    Driver->>Back: Driver Accepts Trip Request
    Back->>Rider: Share Driver Details (Vehicle Number, Driver Rating, Live Bearing)
    
    Driver->>Rider: Arrives at Pickup Coordinates
    Rider->>Driver: Board vehicle and share 4-Digit Start OTP
    Driver->>Back: Validate Start OTP via App Keypad
    Back->>Back: Transition state to TRIP_IN_TRANSIT
    
    Note over Driver,Rider: Live telemetry tracking with automated route deviation and standstill monitoring
    
    Driver->>Back: Arrive at Drop Location and tap End Trip
    Back->>Back: Calculate FASTag automated toll charges and auto-debit UPI or Wallet
    Back-->>Rider: Display Digital Receipt and prompt for Driver Rating and Tip
    Back-->>Driver: Credit Trip Earnings to Driver Payout Ledger
```

---

### 5.5 Vertical 5: Logistics & Parcel Delivery Workflow
```mermaid
flowchart TD
    BookParcel["Customer / Business User books Parcel on Customer App"] --> ModeSelect{"Select Logistics Service Category"}
    
    ModeSelect -->|Hyperlocal Intra-City < 25km| IntraCity["Two-Wheeler Point-to-Point Courier"]
    ModeSelect -->|Inter-City Freight| InterCity["Three-Wheeler / Cargo Truck Freight"]
    
    IntraCity --> VolCalc["Calculate Gross Weight vs Volumetric Weight (L x W x H / 5000)"]
    InterCity --> VolCalc
    
    VolCalc --> RestrictCheck["Sender signs Digital Checkbox: No Cash, Jewelry, Flammables, or Contraband"]
    RestrictCheck --> GenerateQR["Generate Digital QR Waybill for package labeling"]
    
    GenerateQR --> DriverAssign["Dispatch Nearest Logistics Partner"]
    DriverAssign --> SenderPickup["Partner arrives at Sender premises, verifies package, captures photo"]
    
    SenderPickup --> RouteTransit{"Is Hyperlocal or Inter-City?"}
    RouteTransit -->|Hyperlocal| DirectTransit["Direct transit to Recipient address via turn-by-turn GPS"]
    RouteTransit -->|Inter-City| HubConsolidate["Transported to Hub Ingestion to Line-Haul Transport to Destination Hub"]
    
    DirectTransit --> RecipientDoor["Arrive at Recipient Doorstep"]
    HubConsolidate --> RecipientDoor
    
    RecipientDoor --> VerifyOTP["Recipient provides Secure 4-Digit Delivery OTP sent via SMS/WhatsApp"]
    VerifyOTP --> Delivered["Shipment closed as DELIVERED and Proof of Delivery archived in cloud"]
```

---

### 5.6 Vertical 6: On-Demand Home Services Workflow
```mermaid
flowchart TD
    SelectService["Customer selects Home Service (AC Repair, Plumber, Electrician)"] --> RateCard["View Standardized Rate Card (Inspection fee and labor rate scope)"]
    RateCard --> SlotSelect["Select 2-Hour Arrival Window on Multi-Day Calendar"]
    SlotSelect --> TechAssign["Specialist Engine dispatches Verified, Background-Checked Technician"]
    
    TechAssign --> TechArrival["Technician arrives in uniform with digital toolkit"]
    TechArrival --> StartJob["Customer shares 4-Digit Job Start OTP"]
    StartJob --> Inspection["Technician inspects equipment and identifies required work scope"]
    
    Inspection --> ExtraPartsCheck{"Are Extra Spare Parts Required?"}
    
    ExtraPartsCheck -->|No Extra Parts| StandardWork["Technician executes standard service scope"]
    
    ExtraPartsCheck -->|Yes Extra Parts| DigitalQuote["Technician builds In-App Spare Parts Quotation on Workforce App"]
    DigitalQuote --> PushPrompt["Customer App receives instant push modal with price breakdown"]
    PushPrompt --> CustApproval{"Customer Digital Decision"}
    
    CustApproval -->|Rejected| AbortExtra["Extra parts cancelled and standard inspection fee applies"]
    CustApproval -->|Approved| ResumeWork["Customer digitally approves and Technician proceeds with replacement"]
    
    StandardWork --> PhotoQC["Technician captures mandatory Before and After photos"]
    ResumeWork --> PhotoQC
    
    PhotoQC --> FinishOTP["Customer validates work completion via Job Completion OTP"]
    FinishOTP --> Warranty["Platform issues 30-Day Digital Service Warranty Certificate in Customer App"]
```

---

### 5.7 Vertical 7: Healthcare Services Workflow
```mermaid
sequenceDiagram
    autonumber
    actor Patient as Customer App
    participant Gateway as Healthcare Gateway
    actor Doctor as Doctor Console (RMP)
    participant ABDM as ABDM Sandbox / ABHA
    actor Phleb as Phlebotomist (Workforce App)

    alt Video Teleconsultation Channel
        Patient->>Gateway: Search Doctor by Specialty and Select Teleconsult Slot
        Gateway->>ABDM: Verify Patient ABHA ID and Doctor Medical Council Registration
        Patient->>Doctor: Join Encrypted WebRTC Video Consultation Room
        Doctor->>Doctor: Review symptoms and prescribe permissible List O and List A drugs
        Doctor->>Gateway: Submit cryptographically signed digital prescription
        Gateway->>Patient: Save Signed PDF in Patient's Encrypted Health Locker
        
        opt External Licensed Pharmacy Fulfillment
            Patient->>Gateway: Opt to order prescribed medications
            Gateway->>Gateway: Route PDF to Licensed Partner Pharmacy via API
            Note over Gateway: Licensed retail pharmacist tele-verifies prescription before dispensing
        end
    else Home Diagnostic Sample Collection Channel
        Patient->>Gateway: Book Full Body Blood Checkup (Select fasting morning slot)
        Gateway->>Phleb: Assign certified phlebotomist with temperature-controlled cold carrier
        Phleb->>Patient: Arrive at home, draw blood samples, and scan barcoded vacutainer tubes
        Phleb->>Gateway: Hand over samples to accredited partner diagnostic laboratory
        Gateway->>Patient: Encrypted Diagnostic Report PDF delivered to Health Locker within 24 hours
    end
```

---

### 5.8 Vertical 8: Education & Tutoring Enrollment Workflow
```mermaid
flowchart TD
    BrowseTutor["Parent/Student browses Tutors, Coaching Institutes, or Exam Batches"] --> BookDemo["Schedule Free or Paid Demo Class Session"]
    BookDemo --> AttendDemo["Student attends interactive WebRTC live demo classroom"]
    
    AttendDemo --> Satisfied{"Proceed with Course Enrollment?"}
    Satisfied -->|No| Feedback["Collect feedback and recommend alternative tutors"]
    
    Satisfied -->|Yes| PlanChoice["Select Payment Schedule: Full Term Upfront vs. Monthly Installments"]
    
    PlanChoice -->|Monthly Installments| Mandate["Parent sets up recurring UPI Autopay / e-NACH mandate"]
    PlanChoice -->|Full Payment| UpfrontPay["One-time payment via UPI / NetBanking"]
    
    Mandate --> Enrolled["Student added to active batch roster, digital timetable and notes library"]
    UpfrontPay --> Enrolled
    
    Enrolled --> DailyClass["Student joins live scheduled lectures and submits digital homework"]
    DailyClass --> AttendanceAlert["Teacher marks attendance and automated SMS sent to parents if absent"]
    DailyClass --> ProgressReports["Quarterly mock test assessments and digital report cards published"]
```

---

### 5.9 Vertical 9: Hotel & Accommodation Booking Workflow
```mermaid
flowchart TD
    SearchHotel["Customer searches Hotel by City, Landmark, or Geo-Radius"] --> DateSelect["Select Check-In / Check-Out Dates and Room Category"]
    DateSelect --> HoldLock["10-Minute Real-Time Room Inventory Reservation Lock"]
    
    HoldLock --> Prepay{"Payment Selection"}
    Prepay -->|Prepaid Online| OnlinePay["Settle room tariff via UPI / Card"]
    Prepay -->|Pay at Hotel| VerifyCard["Verify customer trust score and guarantee reservation"]
    
    OnlinePay --> BookingOK["Booking Confirmed and Instant PDF Voucher generated"]
    VerifyCard --> BookingOK
    
    BookingOK --> KycCheck{"Is Guest an Indian Domestic Citizen?"}
    
    KycCheck -->|Yes Domestic| DomesticKYC["Pre-arrival ID upload presented as optional feature"]
    KycCheck -->|No Foreign Passport| ForeignFormC["App enforces mandatory Form C immigration fields (Passport, Visa, Port of Entry)"]
    
    DomesticKYC --> ReceptionArrival["Guest arrives at hotel front desk"]
    ForeignFormC --> TransmitBoI["Hotelier Extranet transmits Form C data to BoI FRRO portal within 24 hours"]
    TransmitBoI --> ReceptionArrival
    
    ReceptionArrival --> CheckInQR["Front desk scans digital voucher QR code and hands over room keycard"]
    CheckInQR --> StayComplete["Guest completes stay and folio settled upon check-out"]
```

---

## 6. Financial Treasury, Double-Entry Ledger & Split-Invoicing Flow

Every transaction enforces 64-bit integer minor unit (**Paise**) arithmetic and automatic tax entity bifurcation:

```mermaid
flowchart TD
    CustomerCharge["Customer Payment Settled via UPI Intent: ₹1,000 (100000 Paise)"] --> Router{"Evaluate Tax Invoicing Rules"}
    
    Router -->|Food Delivery OR Ride Hailing| Sec95_Flow["Section 9(5) CGST Act: Platform is Deemed Supplier"]
    Router -->|Grocery, E-Commerce, Registered Hotels, Registered Techs| Sec52_Flow["Section 52 CGST Act: Merchant is Legal Supplier"]
    
    subgraph Sec95_Invoicing["Section 9(5) Tax Invoicing"]
        Sec95_Flow --> Inv_Plat["Generate Platform Tax Invoice (Platform GSTIN)<br/>• Base Service: ₹900 (Taxed at 5% GST)<br/>• Platform Fee: ₹50 (Taxed at 18% GST)<br/>• Delivery Fee: ₹50 (Taxed at 18% GST)"]
        Inv_Plat --> Remit_Direct["Platform remits all GST directly to Government. Zero TCS deducted."]
    end
    
    subgraph Sec52_Invoicing["Section 52 Tax Invoicing"]
        Sec52_Flow --> Inv_Merch["Generate Merchant Tax Invoice (Merchant GSTIN)<br/>• Product Value: ₹900 (Taxed per HSN code)"]
        Sec52_Flow --> Inv_PlatFee["Generate Separate Platform Fee Invoice (Platform GSTIN)<br/>• Platform Convenience Fee: ₹100 (Taxed at 18% GST)"]
        Inv_Merch --> DeductTCS["Platform deducts exactly 0.5% GST TCS (0.25% CGST + 0.25% SGST) for GSTR-8"]
    end
    
    Remit_Direct --> DoubleEntry["PostgreSQL Double-Entry Immutable Ledger Write"]
    DeductTCS --> DoubleEntry
    
    subgraph LedgerWrites["Balanced Double-Entry Journal (Paise)"]
        DoubleEntry --> DebitCash["DEBIT: Gateway Clearing Account (Asset) +100000 Paise"]
        DoubleEntry --> CreditMerchant["CREDIT: Merchant Payout Escrow (Liability) +85000 Paise"]
        DoubleEntry --> CreditRider["CREDIT: Rider Compensation Ledger (Liability) +5000 Paise"]
        DoubleEntry --> CreditRev["CREDIT: Platform Take-Rate Revenue (Equity) +10000 Paise"]
    end
    
    DoubleEntry --> T1Settlement["Automated T+1 Payout Batch via IMPS or NEFT<br/>(Deducting 1% TDS under Section 194-O)"]
```

---

## 7. High-Scale Concurrency, Anti-Spoofing & Persistent Idempotency Flow

```mermaid
sequenceDiagram
    autonumber
    actor Driver as Workforce Partner (Dual-Mode)
    participant Redis as Redis Cluster (L1 Lease Engine)
    participant Dispatch as Dispatch Micro-Service
    participant DB as PostgreSQL (L2 Persistent Outbox)
    participant Sec as Anti-Spoofing Security Engine

    Driver->>Sec: Captures GPS telemetry packet (Lat, Lng, Bearing)
    Sec->>Sec: Verify location.isMock() == false
    Sec->>Sec: Verify Play Integrity token (bootloader locked, no Magisk/Frida)
    Sec->>Sec: Validate GNSS Doppler variance and kinematic speed under 120 km/h
    Sec->>Dispatch: Forward verified coordinate packet
    
    Note over Dispatch,Redis: Dispatcher targets dual-mode driver for new assignment
    
    Dispatch->>Redis: Execute Atomic Lua Script with Monotonic Counter
    Redis->>Redis: INCR dispatch:fencing:counter -> Token: 10921
    Redis->>Redis: SET driver:state:DRV_501 "OFFERED_LOCK" EX 30
    Redis-->>Dispatch: Lease Acquired (Fencing Token: 10921, TTL: 30s)
    
    Dispatch->>DB: INSERT INTO dispatch_assignments (id, driver_id, fencing_token, status, expires_at)
    DB-->>Dispatch: Committed in PostgreSQL (Status: 'OFFERED')
    
    Dispatch->>Driver: Push Task Offer Card (30-Second Acceptance Bar)
    
    alt Driver Accepts Offer within 30s
        Driver->>Dispatch: POST /dispatch/accept (Task ID, Fencing Token: 10921)
        Dispatch->>DB: UPDATE dispatch_assignments SET status = 'CONFIRMED' WHERE fencing_token = 10921 AND expires_at > NOW()
        DB-->>Dispatch: Row Updated Successfully
        Dispatch->>Redis: SET driver:state:DRV_501 "ENGAGED" (Indefinite Lock)
        Dispatch-->>Driver: Launch Navigation Screen
    else Driver Lapses or Network Drops (> 30s)
        Note over Redis: Redis Key expires automatically at 30 seconds
        DB->>Dispatch: BullMQ background recovery worker marks assignment EXPIRED
        Dispatch->>Redis: SET driver:state:DRV_501 "AVAILABLE"
        Dispatch->>Dispatch: Re-route task to next closest partner
    end
```

---

## 8. Master Visual Document Index & References

This visual hierarchy blueprint coordinates directly with the complete project documentation suite:

| Document Reference | Full File Path | Primary Visual & Architectural Coverage |
|:---|:---|:---|
| **Master Project Charter** | [`docs/01_project_charter/master_project_charter.md`](file:///Users/firozmohammad/DigiEmperor/all_in_one/docs/01_project_charter/master_project_charter.md) | Ecosystem Business Objectives & 9 Verticals Scope |
| **Product Breakdown Structure** | [`docs/02_product_breakdown_structure/product_breakdown_structure.md`](file:///Users/firozmohammad/DigiEmperor/all_in_one/docs/02_product_breakdown_structure/product_breakdown_structure.md) | 4-Level Deliverable Hierarchy & App Traceability |
| **Business Requirements Document** | [`docs/03_business_requirements_document/business_requirements_document.md`](file:///Users/firozmohammad/DigiEmperor/all_in_one/docs/03_business_requirements_document/business_requirements_document.md) | Commercial Take Rates, Commission Matrices & NFRs |
| **Remediation Plan V1.1** | [`docs/05_remediation_plan/enterprise_remediation_plan_v1.1.md`](file:///Users/firozmohammad/DigiEmperor/all_in_one/docs/05_remediation_plan/enterprise_remediation_plan_v1.1.md) | Authoritative Statutory GST, COD & Concurrency Remediations |
| **Repository README** | [`README.md`](file:///Users/firozmohammad/DigiEmperor/all_in_one/README.md) | Master 5-Step Execution Roadmap & Document Index |

---

## 9. Document Sign-Off Notice

* **Document Identifier:** VHB-IND-V1.1
* **Syntax Validation:** All Mermaid diagrams utilize GitHub-native compatible syntax (clean labels, `<br/>` line breaks, zero semicolons, zero unescaped arrows).
* **Next Action:** Awaiting executive approval on Remediation Decisions `DEC-01` through `DEC-07` to begin foundational document updates and Final PRD authoring.
