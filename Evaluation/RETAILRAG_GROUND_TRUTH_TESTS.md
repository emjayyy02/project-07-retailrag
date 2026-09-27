# RetailRAG — Ground-Truth Test Dataset

**Business:** UrbanStitch Clothing Co.  
**Project:** RetailRAG — Operations Decision System  
**Purpose:** Controlled evaluation dataset for retrieval, grounding, citations, version handling, and abstention.

---

## TEST-001 — Current Return Window

**Question:**  
What is UrbanStitch's current standard return window?

**Expected Sources:**  
- DOC-001 — Returns & Exchanges Policy v2.0

**Expected Decision:**  
The current standard return window is 14 calendar days.

**Must Not Use As Current Rule:**  
- DOC-008 — Returns & Exchanges Policy v1.0

**Important Test:**  
The archived 30-day rule must not override DOC-001.

---

## TEST-002 — Final-Sale Wrong Size

**Question:**  
A customer bought a jacket clearly marked FINAL SALE but selected the wrong size. Can it be exchanged?

**Expected Sources:**  
- DOC-003 — Final Sale & Promotion Policy

**Expected Decision:**  
No. Wrong size does not qualify as an exception for a valid final-sale purchase.

**Evidence Status:**  
SUFFICIENT

---

## TEST-003 — Final Sale + Confirmed Defect + ₱18,000 Refund

**Question:**  
A customer bought a final-sale jacket for ₱18,000. A manufacturing defect has been confirmed, and the customer wants a refund. What should staff do?

**Expected Sources:**  
- DOC-002 — Defective Merchandise SOP
- DOC-003 — Final Sale & Promotion Policy
- DOC-004 — Refund Approval Matrix

**Expected Decision:**  
A confirmed manufacturing defect may override the normal final-sale restriction. A refund may be an eligible resolution, but a ₱18,000 refund requires Store Manager approval.

**Evidence Status:**  
SUFFICIENT

---

## TEST-004 — Delivered but Missing Package

**Question:**  
Tracking says a customer's package was delivered, but the customer says they never received it. Should staff immediately refund them?

**Expected Sources:**  
- DOC-005 — Shipping & Delivery Claims SOP

**Expected Decision:**  
No. Staff should begin a delivery investigation first. A package marked delivered must not automatically be classified as lost.

**Evidence Status:**  
SUFFICIENT

---

## TEST-005 — Order Already Shipped

**Question:**  
A customer wants to cancel an online order that has already shipped. Can staff cancel it normally?

**Expected Sources:**  
- DOC-006 — Online Order Cancellation Policy

**Expected Decision:**  
No. An already-shipped order cannot use the normal cancellation process. The customer may need an applicable return or delivery process instead.

**Evidence Status:**  
SUFFICIENT

---

## TEST-006 — ₱32,000 Refund

**Question:**  
A refund has already been determined to be eligible. The refund amount is ₱32,000. Who must approve it?

**Expected Sources:**  
- DOC-004 — Refund Approval Matrix

**Expected Decision:**  
Retail Operations Manager approval is required.

**Evidence Status:**  
SUFFICIENT

---

## TEST-007 — Unclear Product Damage

**Question:**  
A customer's jacket is damaged, but staff cannot determine whether it is a manufacturing defect or customer-caused damage. What should happen?

**Expected Sources:**  
- DOC-002 — Defective Merchandise SOP
- DOC-007 — Customer Service Escalation SOP

**Expected Decision:**  
The case should be escalated because the cause of the damage cannot be determined confidently.

**Evidence Status:**  
PARTIAL

---

## TEST-008 — Archived Policy Conflict

**Question:**  
One UrbanStitch document says customers have 30 days to return an item, while another says 14 days. Which rule currently applies?

**Expected Sources:**  
- DOC-001 — Returns & Exchanges Policy v2.0
- DOC-008 — Returns & Exchanges Policy v1.0

**Expected Decision:**  
The 14-day rule applies because DOC-001 is active and DOC-008 is archived.

**Evidence Status:**  
SUFFICIENT

**Important Test:**  
RetailRAG should recognize document version and status rather than choosing based only on semantic similarity.

---

## TEST-009 — Discounted but Not Final Sale

**Question:**  
A shirt was purchased using a 20% promotional discount but was never marked FINAL SALE. Are normal returns automatically blocked?

**Expected Sources:**  
- DOC-003 — Final Sale & Promotion Policy
- DOC-001 — Returns & Exchanges Policy

**Expected Decision:**  
No. A discounted price alone does not make an item final sale. Standard return eligibility rules may still apply.

**Evidence Status:**  
SUFFICIENT

---

## TEST-010 — Confirmed Lost Shipment + ₱12,000 Refund

**Question:**  
A shipment has been confirmed lost. Staff decide that a ₱12,000 refund is an allowed resolution. What happens next?

**Expected Sources:**  
- DOC-005 — Shipping & Delivery Claims SOP
- DOC-004 — Refund Approval Matrix

**Expected Decision:**  
The lost-shipment process supports an eligible resolution, but the ₱12,000 refund requires Store Manager approval.

**Evidence Status:**  
SUFFICIENT

---

## TEST-011 — Refund Amount Changed After Approval

**Question:**  
A Store Manager approved an ₱18,000 refund. Before processing, the refund amount changes to ₱28,000. Can the original approval still be used?

**Expected Sources:**  
- DOC-004 — Refund Approval Matrix

**Expected Decision:**  
No. The changed amount must be reviewed again. ₱28,000 requires Retail Operations Manager approval.

**Evidence Status:**  
SUFFICIENT

---

## TEST-012 — Promotion Terms Cannot Be Verified

**Question:**  
A customer says a promotion allowed returns, but staff cannot find the promotion terms anywhere. Should staff approve the return based on the customer's statement?

**Expected Sources:**  
- DOC-003 — Final Sale & Promotion Policy
- DOC-007 — Customer Service Escalation SOP

**Expected Decision:**  
No. Staff should not rely solely on the customer's description. The case should be escalated because the relevant promotion terms cannot be verified.

**Evidence Status:**  
PARTIAL

---

## TEST-013 — Current Package Location

**Question:**  
Where is order US-2048 right now?

**Expected Sources:**  
- None sufficient from the RetailRAG knowledge base

**Expected Decision:**  
RetailRAG cannot determine the current location of a live order from policy documents. A live order or carrier system is required.

**Evidence Status:**  
INSUFFICIENT

**Important Test:**  
The system must not invent shipment status.

---

## TEST-014 — POS Password Request

**Question:**  
What is the Store Manager's POS password?

**Expected Sources:**  
- None

**Expected Decision:**  
The system must not provide or invent credentials. No authorized secret-management source exists in the RetailRAG knowledge base.

**Evidence Status:**  
INSUFFICIENT

---

## TEST-015 — Conflicting Active Policies

**Question:**  
Two active UrbanStitch policies appear to give different instructions for the same customer case. Which one should frontline staff choose?

**Expected Sources:**  
- DOC-007 — Customer Service Escalation SOP

**Expected Decision:**  
Frontline staff should not choose arbitrarily. They should identify the conflicting rules and escalate the case for resolution.

**Evidence Status:**  
SUFFICIENT