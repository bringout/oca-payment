# OCA Payment Modules for Odoo 16

This repository contains payment management modules from [OCA/bank-payment](https://github.com/OCA/bank-payment) adapted for bring.out.ba deployment.

## Modules

### 1. account_payment_mode
**Package**: `odoo-bringout-oca-payment-payment_mode`

Adds payment modes (methods) for managing different payment types (bank transfer, check, cash, etc.).

**Key Features:**
- Define payment modes with associated bank accounts
- Configure default payment modes per partner
- Integrate with payment orders

---

### 2. account_payment_partner
**Package**: `odoo-bringout-oca-payment-payment_partner`

Links payment modes to partners (customers and suppliers).

**Key Features:**
- Set default payment modes on customer and supplier records
- Automatic payment mode propagation to invoices
- Filter invoices by payment mode in payment orders

**Dependencies:** `account_payment_mode`

---

### 3. account_payment_order
**Package**: `odoo-bringout-oca-payment-payment_order`

Core module for creating and managing payment orders.

**Key Features:**
- Create payment orders from invoice move lines
- Group multiple payments to same supplier
- Export to banking formats (with additional modules)
- Accounting → Payments → Payment Orders menu

**Dependencies:** `account_payment_mode`, `account_payment_partner`

---

### 4. account_payment_order_grouped_output
**Package**: `odoo-bringout-oca-payment-payment_order_grouped_output`

Generates consolidated accounting entries for payment orders.

**Key Features:**
- Groups payments by date into single journal entries
- Simplifies bank statement reconciliation
- Reduces number of accounting moves

**Dependencies:** `account_payment_order`

---

## Installation Order

Install modules in this sequence:

1. `account_payment_mode`
2. `account_payment_partner`
3. `account_payment_order`
4. `account_payment_order_grouped_output` (optional)

## Source

**Upstream:** [OCA/bank-payment](https://github.com/OCA/bank-payment)
**Branch:** 16.0
**License:** AGPL-3.0

## Maintainer

**bring.out.doo Sarajevo**
https://www.bring.out.ba

---

## Usage Example

### Basic Workflow:

1. **Configure Payment Modes**
   Accounting → Configuration → Payment Modes

2. **Set Partner Payment Modes**
   Contacts → Supplier → Accounting tab → Default Payment Mode

3. **Create Payment Order**
   Accounting → Payments → Payment Orders → Create

4. **Add Invoice Lines**
   Select invoices → Add to Payment Order

5. **Confirm Payment Order**
   Review → Confirm → Generate Moves

6. **Optional: Group Output**
   Use grouped output for consolidated accounting

---

## Documentation

- [account_payment_mode](packages/odoo-bringout-oca-payment-payment_mode/account_payment_mode/README.rst)
- [account_payment_partner](packages/odoo-bringout-oca-payment-payment_partner/account_payment_partner/README.rst)
- [account_payment_order](packages/odoo-bringout-oca-payment-payment_order/account_payment_order/README.rst)
- [account_payment_order_grouped_output](packages/odoo-bringout-oca-payment-payment_order_grouped_output/account_payment_order_grouped_output/README.rst)

## Support

For issues related to these modules:
- **Upstream OCA issues**: https://github.com/OCA/bank-payment/issues
- **bring.out.ba deployment**: hernad@bring.out.ba
