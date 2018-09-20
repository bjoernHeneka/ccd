## Bad
```go
pPrice := purchasingPrice.calculatedPrice
percentage = helper.GetPercentage(pPrice)
conatraints := GetConstraints()

// add transport costs to purchasing price
if (base.ProductInfo,.Weight > 30.00 && *minPrice > 20.00) || (base.ProductInfo,.CargoType == models.CARGO_TYPE_CARRIER) {
    *pPrice += viper.GetFloat64("jacob.cargoFees.carrier")
    logger.Log.Infof("[CALCULATION][INFO] Add %v EUR to purchasing price because of cargo type Carrier", viper.GetFloat64("jacob.cargoFees.carrier"))
} else if base.ProductInfo,.CargoType == models.CARGO_TYPE_BULK {
    *pPrice += viper.GetFloat64("jacob.cargoFees.bulk")
    logger.Log.Infof("[CALCULATION][INFO] Add %v EUR to purchasing price because of cargo type BULK", viper.GetFloat64("jacob.cargoFees.bulk"))
}

// Order < 200
for _, constraint := range constraints {
    if (constraint.ExecutionOrder < 200 && constraint.ChannelId == channelId) {
        logger.Log.Error(constraint.ExecutionOrder)
        switch strings.ToLower(constraint.Type) {
            case models.CONSTRAINT_TYPE_FIX:
                pPrice = constraint.Price
                logger.Log.Infof("Calculating with Fixprice: %v and Order: %d", constraint.Price, constraint.ExecutionOrder)
                break
            case models.CONSTRAINT_TYPE_RELATIVE:
                pPrice = pPrice * constraint.Factor
                logger.Log.Infof("Calculating with Factor: %v and Order: %d", constraint.Factor, constraint.ExecutionOrder)
                break
            case models.CONSTRAINT_TYPE_ABSOLUTE:
                pPrice = pPrice + constraint.Price
                logger.Log.Infof("Calculating with Absolute addition: +%v and Order: %d", constraint.Price, constraint.ExecutionOrder)
            default:
                logger.Log.Warnf("[CALCULATION][WARN] Unknown constrsaint type %v", constraint.Type)
        }
    }
}


// Order == 200
pPrice = AddCalculationFactor(pPrice, percentage)

if percentage > 0 {
    pPrice := input * calcFactor
    logger.Log.Infof("Calculate with %v * %v = %v.", input, calcFactor, result)
} else {
    pPrice = pPrice
}

// Order > 200
for _, constraint := range constraints {
    if (constraint.ExecutionOrder > 200 && constraint.ChannelId == channelId) {
        logger.Log.Error(constraint.ExecutionOrder)
        switch strings.ToLower(constraint.Type) {
            case models.CONSTRAINT_TYPE_FIX:
                pPrice = constraint.Price
                logger.Log.Infof("Calculating with Fixprice: %v and Order: %d", constraint.Price, constraint.ExecutionOrder)
                break
            case models.CONSTRAINT_TYPE_RELATIVE:
                pPrice = pPrice * constraint.Factor
                logger.Log.Infof("Calculating with Factor: %v and Order: %d", constraint.Factor, constraint.ExecutionOrder)
                break
            case models.CONSTRAINT_TYPE_ABSOLUTE:
                pPrice = pPrice + constraint.Price
                logger.Log.Infof("Calculating with Absolute addition: +%v and Order: %d", constraint.Price, constraint.ExecutionOrder)
            default:
                logger.Log.Warnf("[CALCULATION][WARN] Unknown constrsaint type %v", constraint.Type)
        }
    }
}

```