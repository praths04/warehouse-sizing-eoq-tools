# Warehouse Sizing & EOQ: Two Python Tools for Inventory Decisions

Two small Python tools that turn common inventory questions into a number you can act on:

1. **Warehouse sizing:** how much private warehouse space to build, and how much to rent, when monthly demand fluctuates.
2. **EOQ with tiered discounts:** the lowest-cost order quantity when a supplier offers price breaks at different quantities.

**Tools:** Python (NumPy, SciPy, Matplotlib), Jupyter

---

## Tool 1: Warehouse sizing

**Question:** If demand changes month to month, how many units of private warehouse space minimize total annual cost, given that anything the private warehouse can't hold has to be rented?

**How it works**

- You enter 12 months of sales volume.
- The tool converts each month's volume into the space it needs, fills the private warehouse first, and rents the rest.
- It adds up four monthly costs: fixed (amortized construction plus annual fixed cost), variable handling in the private warehouse, rented storage, and rented handling.
- `scipy.optimize.minimize` finds the number of 10,000 sq ft units that gives the lowest total cost.
- It prints a month-by-month cost table and plots total cost against the number of units (1 to 7), with the optimum marked.

**Assumptions:** the cost parameters (construction cost per sq ft, amortization years, annual fixed cost, variable cost per kg, rental storage and handling rates, inventory turnover, stack height and space conversion factor) are set at the top of the notebook. Change them to match your own situation.

## Tool 2: EOQ with tiered supplier discounts

**Question:** A supplier gives a lower unit price the more you order. Which price tier and order quantity minimize total cost?

**How it works**

- You enter annual demand, ordering cost, carrying cost as a percentage of unit cost, the unit cost, and each quantity slab with its discount.
- For each slab, the tool calculates the discounted unit cost, the carrying cost, and the classic EOQ, `sqrt(2 x demand x ordering cost / carrying cost)`.
- If the EOQ falls below the minimum quantity of a slab, it searches for the cheapest order quantity that still qualifies for that slab's price.
- It then compares total cost (purchase + carrying + ordering) across all slabs and reports the slab and order quantity with the lowest total.

## Files

| File | What it is |
|---|---|
| `warehouse_sizing_tool.ipynb` | Warehouse sizing optimizer |
| `eoq_quantity_discount_tool.ipynb` | EOQ calculator with tiered discounts |

## How to run

```bash
pip install numpy scipy matplotlib jupyter
jupyter notebook
```

Open a notebook, run the cell, and answer the prompts for your own inputs.

## Limitations

- Both tools are input-driven (they prompt for values) and have not been checked against real company data.
- In the EOQ tool, a slab entered as a range is averaged into a single threshold, and the two range values should be separated by a space (for example `500 1000`).
- The warehouse tool's cost parameters are fixed assumptions in the code, so results are only as good as those assumptions.

## Author

Prathiba Reddy, MS in Business Analytics & AI, Johns Hopkins Carey Business School
[LinkedIn](https://www.linkedin.com/in/prathiba-reddy-namireddy) | [Portfolio](https://6a38b7b1cee129ca7a613700--comforting-queijadas-d1f251.netlify.app)
