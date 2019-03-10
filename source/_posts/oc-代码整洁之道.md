---
title: oc 代码整洁之道
date: 2019-03-11 01:16:26
tags: oc
categories: 代码整洁
---


=====================================================================
———————————————<font size=4 color=orange> oc 代码编写</font>———————————————

* 1、见文知义，写的方法要知道要干嘛，千万不要在这样的set方法里面设置其他东西
```
- (void)setSelectedProduct:(ProductData *)selectedProduct
{
    if (_selectedProduct) {
        NSInteger index = [self.productArray indexOfObject:_selectedProduct];
        NSIndexPath * indexPath = [NSIndexPath indexPathForRow:index inSection:0];
        PurchaseItemCell * cell = (PurchaseItemCell *)[self.collectionView cellForItemAtIndexPath:indexPath];
        cell.wkSelected = NO;
    }
    _selectedProduct = selectedProduct;
    if (_selectedProduct) {
        NSInteger index = [self.productArray indexOfObject:_selectedProduct];
        NSIndexPath * indexPath = [NSIndexPath indexPathForRow:index inSection:0];
        PurchaseItemCell * cell = (PurchaseItemCell *)[self.collectionView cellForItemAtIndexPath:indexPath];
        cell.wkSelected = YES;
    }
}

```

