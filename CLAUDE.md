# OCA Payment Modules - Development Notes

## Source Information

**Upstream Repository:** https://github.com/OCA/bank-payment
**Branch:** 16.0
**Clone Date:** 2025-11-12
**License:** AGPL-3.0

## Package Structure

Each package contains a single Odoo module from OCA/bank-payment:

```
packages/
├── odoo-bringout-oca-payment-payment_mode/
│   └── account_payment_mode/          # Odoo module
├── odoo-bringout-oca-payment-payment_partner/
│   └── account_payment_partner/       # Odoo module
├── odoo-bringout-oca-payment-payment_order/
│   └── account_payment_order/         # Odoo module
└── odoo-bringout-oca-payment-payment_order_grouped_output/
    └── account_payment_order_grouped_output/  # Odoo module
```

## Module Dependencies

```
account_payment_mode (base)
    ↓
account_payment_partner
    ↓
account_payment_order
    ↓
account_payment_order_grouped_output
```

## Deployment

### Local Development
```bash
# Sync to odoonix
~/src/bringout/0/scripts/odoonix_rsync.py account_payment_mode
~/src/bringout/0/scripts/odoonix_rsync.py account_payment_partner
~/src/bringout/0/scripts/odoonix_rsync.py account_payment_order
~/src/bringout/0/scripts/odoonix_rsync.py account_payment_order_grouped_output
```

### Production
```bash
# Install in order:
~/src/bringout/0/scripts/upgrade_production_nix_service.py \
  --module account_payment_mode \
  --module account_payment_partner \
  --module account_payment_order \
  --module account_payment_order_grouped_output \
  --install
```

## Use Case

**Problem:** Merge multiple payments to same supplier into one payment order

**Solution:** Use `account_payment_order` to create payment orders that group multiple invoices

**Workflow:**
1. Go to: Accounting → Payments → Payment Orders
2. Create new payment order
3. Select move lines (invoices) from same supplier
4. Confirm → Creates grouped payment
5. Optional: Use grouped_output for consolidated accounting moves

## Upstream Updates

To update from OCA:
```bash
cd /tmp
git clone -b 16.0 https://github.com/OCA/bank-payment.git
# Compare and merge changes manually
```

## Author

**Developer:** Ernad Husremović (hernad@bring.out.ba)
**Company:** bring.out.doo Sarajevo, BiH
**Website:** https://www.bring.out.ba
**Date:** 2025-11-12
