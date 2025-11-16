# Procurement Management System -- Technical Documentation

## 1. Introduction

### 1.1 Purpose

This document provides a clear explanation of the Procurement Management
System architecture, workflow, and all data models. It includes model
purpose, relationships, and a text-based architecture diagram.

### 1.2 Scope

The scope includes: - Procurement Models - Enquiry Models - Vendor
Quotation Models - CST Models - Negotiation Models - PO/DPO Models -
Payment & Invoice Models - Workflow (StageProgress) Models

Only models explicitly provided are included.

## 2. System Architecture

### 2.1 Architecture Diagram (ASCII -- GitHub Compatible)

                       [UserReg]
                           |
                           v
                    [Procurement]
                           |
         ---------------------------------------------
         |                   |                       |
         v                   v                       v
    [Particular]     [BudgetAllocation]      [StageProgress]
         |                                             |
         v                              ------------------------------
    [Quantity]                      [Tracking]                 [Rejection]
         |
         v
       [Units]


    Procurement ---> Enquiry
                        |
                        v
                 [EnquiryFormPR]
                        |
                        v
               [EnquirySupplierPR]
                        |
                        v
                     [Vendor]
                        |
                        v
               [VendorQuotations]
                        |
                        v
           ---------------------------
           |                         |
           v                         v
    [QuotationParticular]   [QuotationQuantity]


                Comparative Statement Flow
                ---------------------------
                        |
                        v
            [ComparativeStatement]
                        |
                        v
            [VendorQuotationDetails]


                Negotiation Flow
                ---------------------------
                        |
                        v
                  [Negotiation]
                        |
                        v
                [DPOParticular]
                        |
                        v
                [Purchase_Order]
                        |
                        v
                  [PaymentData]
                        |
                        v
                [PaymentTracking]
               /                  \
              v                    v
       [PaymentFile]         [Invoice_Files]

## 3. Model Documentation (Standard Format)

### 3.1 UserReg

**Purpose:** Stores employee details and defines approval hierarchy.
**Responsibilities:**
- Maintain user metadata
- Support workflow and approvals

### 3.2 Procurement

**Purpose:** Central model for Purchase Requisitions (PR).
**Responsibilities:**
- Manage procurement request data
- Link requester, project, and category
- Control workflow via StageProgress

### 3.3 Particular

**Purpose:** Item description for each PR.

### 3.4 Quantity

**Purpose:** Quantity of each item under Particular.

### 3.5 Units

**Purpose:** Unit of measurement for quantities.

### 3.6 BudgetAllocation

**Purpose:** Stores budget allocation details for PRs.

### 3.7 StageProgress

**Purpose:** Tracks workflow stages for Procurement.\
**Responsibilities:**
- Maintain status history
- Track approvers and timestamps

### 3.8 Tracking

**Purpose:** Logs workflow actions for auditing.

### 3.9 Rejection

**Purpose:** Stores rejection details and remarks.

## 4. Enquiry Workflow Models

### 4.1 EnquiryFormPR

**Purpose:** Represents enquiry generated from PR.

### 4.2 EnquirySupplierPR

**Purpose:** Vendor assignments for enquiry.

## 5. Vendor Management Models

### 5.1 Vendor

**Purpose:** Vendor master details.

## 6. Quotation Models

### 6.1 VendorQuotations

**Purpose:** Stores vendor quotation header data.

### 6.2 QuotationParticular

**Purpose:** Stores item-level quotation details.

### 6.3 QuotationQuantity

**Purpose:** Price & quantity details for quotation items.

## 7. Comparative Statement (CST) Models

### 7.1 ComparativeStatement

**Purpose:** Compares all vendor quotations for an enquiry.

### 7.2 VendorQuotationDetails

**Purpose:** Detailed comparison per vendor per item.

## 8. Negotiation Models

### 8.1 Negotiation

**Purpose:** Stores negotiation outcomes and revised prices.

### 8.2 DPOParticular

**Purpose:** Items selected for DPO after negotiation.

## 9. Purchase Order & Payment Models

### 9.1 Purchase_Order

**Purpose:** Represents final PO after negotiation.

### 9.2 PaymentData

**Purpose:** Payment initiation details for PO.

### 9.3 PaymentTracking

**Purpose:** Tracks payment stages and statuses.

### 9.4 PaymentFile

**Purpose:** Stores payment proofs.

### 9.5 Invoice_Files

**Purpose:** Stores vendor invoices.
