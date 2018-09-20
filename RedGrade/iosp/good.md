## Good
```go
pPrice := purchasingPrice.calculatedPrice
percentage := helper.GetPercentage(pPrice)
conatraints := GetConstraints()

// add transport costs to purchasing price
AddTransportCosts(base.ProductInfo, &pPrice)

// Order < 200
sellingPrice = AddPreConstraint(pPrice, conatraints, DIRECT_CHANNEL_ID)

// Order == 200
sellingPrice = AddCalculationFactor(pPrice, percentage)

// Order > 200
sellingPrice = AddPostConstraint(pPrice, conatraints, DIRECT_CHANNEL_ID)

```