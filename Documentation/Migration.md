# Migration from RxSwift 1.9 to RxSwift 2.0

The migration should be pretty straightforward. Changes are mostly cosmetic, so all features are still there.

* Find replace all `>- ` to `.`
* Find replace all `variable` to `shareReplay(1)`
* Find replace all `catch` to `catchErrorJustReturn`
* Find replace all `returnElement` to `Observable.just`
* Find replace all `failWith` to `Observable.error`
* Find replace all `never` to `Observable.never`
* Find replace all `empty` to `Observable.empty`
* Since we've moved from `>-` to `.`, free functions are now methods, so use `.switchLatest()`, `.distinctUntilChanged()`, ... instead of `>- switchLatest`, `>- distinctUntilChanged`
* We've moved from free functions to extensions so it's now `[a, b, c].concat()`, `.merge()`, ... instead of `concat([a, b, c])`, `merge(sequences)`
* Similarly, it's now `subscribe { n in ... }.addDisposableTo(disposeBag)` instead of `>- disposeBag.addDisposable`
* The method `next` on `Variable` is now `value` setter
* If you want to use `UITableView` and/or  `UICollectionView`, this is the basic use case now:

```swift
viewModel.rows
    .bindTo(resultsTableView.rx_itemsWithCellIdentifier("WikipediaSearchCell", cellType: WikipediaSearchCell.self)) { (_, viewModel, cell) in
        cell.viewModel = viewModel
    }
    .addDisposableTo(disposeBag)
```

If you have any doubts about how some concept in RxSwift 2.0 works, check out the [Example app](../RxExample) or playgrounds.
