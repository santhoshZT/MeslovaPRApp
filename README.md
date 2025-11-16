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


# PR Creation Prerequisites & Workflow

## 1. Prerequisites for Generating a Purchase Requisition (PR)

Before creating a PR, the following master data must be configured:

### Step 1 -- Create Roles

Required approval hierarchy roles: - Indentor - Recommending Authority
(RA) - IMM - Accounts - Approving Authority

### Step 2 -- Create Departments

Each department must include: - Department Name - Department Code

### Step 3 -- Create Delivery Types

Configure: - Delivery Name

### Step 4 -- Create Procurement Types

Include: - Procurement Code - Procurement Name

### Step 5 -- Create Locations

Define the full list of applicable locations.

### Step 6 -- Create Tender Types

Setup tender type master data.

### Step 7 -- Create Source of Make

Each source requires: - Source Code - Source Type

### Step 8 -- Create Units

Add all required units of measurement (UOM).

------------------------------------------------------------------------

## 2. Purchase Requisition (PR) Generation Workflow

### 1. PR Creation (Indentor)

-   The Indentor initiates the PR and fills all required fields in the
    PR Form.

### 2. Review by Recommending Authority (RA)

-   After submission, the PR moves to the RA for verification and
    approval.

### 3. RA Approval

-   RA reviews the details and approves the PR.

### 4. PR Forwarded to IMM

-   After RA approval, the PR is sent to the IMM department for further
    processing.

### 5. IMM Review

-   IMM reviews the form and forwards it to the Accounts role.

### 6. Accounts Review

-   Accounts verifies the PR and recommends it to the Approving
    Authority.

### 7. Return & Modification Rules

-   Any higher authority can return the PR to a lower authority.
-   Only the Indentor (original creator) can make modifications.

### 8. Enquiry Form Generation

-   After approval, IMM generates the Enquiry Form.
-   Vendor quotations are uploaded in this stage.

### 9. CST Generation

-   The Comparative Statement (CST) is generated.
-   CST is approved by IMM and recommended to the Indentor.

### 10. Indentor Review

-   Indentor reviews CST and recommends it to RA.
-   If negotiation is required, Indentor triggers negotiation.

### 11. RA Review

-   RA reviews and submits the form, recommending it to IMM.

### 12. Negotiation or DPO Creation

-   If negotiation occurs OR if RA submits, the PR moves to the DPO
    (Draft PO) stage.

### 13. IMM Review for DPO

-   IMM reviews the DPO and recommends it to Accounts.

### 14. Accounts Approval

-   Accounts approves the DPO and cycle may repeat if required.

### 15. Final PO Approval & Sign Upload

-   After final PO approval, the designated user uploads the approved
    and signed copy.

