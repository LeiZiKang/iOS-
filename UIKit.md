# UIViewController

## init

在 Swift 中，自定义视图控制器的 `init` 方法可以让你在创建视图控制器实例时传递一些自定义参数。通常情况下，视图控制器的初始化方法是 `init(nibName:bundle:)` 或 `init(coder:)`，但你也可以添加自己的初始化方法。

以下是如何编写一个自定义的 `init` 方法的示例：

### 示例代码

假设我们要创建一个视图控制器，它在初始化时需要传递一个字符串参数：

```swift
import UIKit

class MyViewController: UIViewController {
    
    // 自定义属性
    var customString: String
    
    // 自定义的初始化方法
    init(customString: String) {
        // 设置自定义属性
        self.customString = customString
        
        // 调用父类的指定初始化方法
        super.init(nibName: nil, bundle: nil)
    }
    
    // 这个初始化方法是必须实现的，用于从 storyboard 或 nib 文件中加载视图控制器
    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        // 设置视图控制器的背景颜色
        view.backgroundColor = .white
        
        // 使用自定义属性
        print("Custom String: \(customString)")
    }
}
```

### 详细步骤解释

1. **定义自定义属性**：
   - 在视图控制器类中定义一个属性来存储初始化时传递的参数。例如，这里我们定义了一个 `customString` 属性。

2. **实现自定义的 `init` 方法**：
   - 实现一个接受自定义参数的初始化方法。在这个方法中，首先设置自定义属性，然后调用父类的指定初始化方法 `super.init(nibName:bundle:)`。
   - 注意：`super.init(nibName:bundle:)` 中的 `nibName` 和 `bundle` 参数可以根据需要设置。如果不使用 nib 文件，可以传递 `nil`。

3. **实现 `required init?(coder:)` 方法**：
   - 这是一个必须实现的方法，用于从 storyboard 或 nib 文件中加载视图控制器。如果你的视图控制器不使用 storyboard 或 nib 文件，可以在这个方法中引发一个运行时错误（如 `fatalError`）。

4. **使用自定义属性**：
   - 在 `viewDidLoad` 或其他生命周期方法中，可以使用自定义属性来配置视图控制器的内容。

### 使用自定义初始化方法

在创建视图控制器实例时，可以使用自定义的 `init` 方法：

```swift
let myViewController = MyViewController(customString: "Hello, World!")
```

然后可以将这个视图控制器实例推入导航控制器或以其他方式展示：

```swift
let navigationController = UINavigationController(rootViewController: myViewController)
present(navigationController, animated: true, completion: nil)
```

通过这种方式，你可以在创建视图控制器实例时传递自定义参数，并在视图控制器中使用这些参数来配置视图。


---

# UITableView与UICollectionView

`UITableView` 和 `UICollectionView` 是 iOS 开发中常用的两个视图组件，它们用于显示和管理列表和网格数据。虽然它们有很多相似之处，但也有一些关键的区别和各自的使用场景。

### UITableView

**特点**：
- **单列显示**：`UITableView` 通常用于显示单列的垂直列表。
- **静态和动态内容**：可以显示静态和动态内容。
- **分区和行**：支持分区（sections）和行（rows），可以在每个分区中显示不同的数据。
- **内置样式**：提供了一些内置的样式，如分组样式（grouped）和纯样式（plain）。

**使用场景**：
- **简单列表**：如联系人列表、消息列表、设置页面等。
- **分区数据**：如分组的联系人列表、分类的新闻列表等。
- **单列数据**：适用于只需要垂直滚动的单列数据。

**示例代码**：

```swift
import UIKit

class MyTableViewController: UITableViewController {
    let data = ["Item 1", "Item 2", "Item 3"]

    override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return data.count
    }

    override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "cell", for: indexPath)
        cell.textLabel?.text = data[indexPath.row]
        return cell
    }
}
```

### UICollectionView

**特点**：
- **多列显示**：`UICollectionView` 可以显示多列的数据，支持复杂的网格布局。
- **自定义布局**：通过 `UICollectionViewLayout` 可以实现高度自定义的布局，如瀑布流布局、环形布局等。
- **灵活性**：比 `UITableView` 更灵活，适用于各种复杂的布局需求。

**使用场景**：
- **网格布局**：如图片库、商品展示等。
- **自定义布局**：需要高度自定义的布局，如时间轴、横向滚动的卡片列表等。
- **多列数据**：适用于需要多列显示的数据。

**示例代码**：

```swift
import UIKit

class MyCollectionViewController: UICollectionViewController {
    let data = ["Item 1", "Item 2", "Item 3"]

    override func collectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int {
        return data.count
    }

    override func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
        let cell = collectionView.dequeueReusableCell(withReuseIdentifier: "cell", for: indexPath)
        cell.contentView.backgroundColor = .blue
        return cell
    }
}
```

### 总结

- **UITableView**：
  - **优点**：简单易用，适合展示单列的列表数据，支持分区。
  - **缺点**：布局相对固定，灵活性较差。

- **UICollectionView**：
  - **优点**：布局灵活，可以实现各种复杂的布局和多列显示。
  - **缺点**：设置和使用相对复杂，需要自定义布局。

选择使用哪一个组件，主要取决于你的数据展示需求和布局复杂度。如果你需要展示简单的单列列表，`UITableView` 是一个很好的选择。如果你需要展示复杂的网格布局或自定义布局，`UICollectionView` 会更加适合。

**Note:**
一般UICollectionView的cell的isSelected尽量不要使用，因为其带有默认的UI样式，建议使用自定义的beSelected属性代替

**Note:**
UICollectionView的数据绑定与UI更新Apple已经写好，当你想要改变UI时，应该改变数据而非直接改变UI

在选中或取消选中 `UICollectionView` 单元格时，`UICollectionView` 不会自动调用 `collectionView(_:cellForItemAt:)` 方法来重新配置单元格。相反，它会调用单元格的 `isSelected` 属性的 `didSet` 方法。因此，如果你在自定义单元格中正确处理了 `isSelected` 属性的变化，UI 会自动更新。

### 自定义单元格的 `isSelected` 属性

确保在自定义单元格中正确处理 `isSelected` 属性的变化。例如：

```swift
import UIKit

class CustomCollectionViewCell: UICollectionViewCell {
    
    override var isSelected: Bool {
        didSet {
            contentView.backgroundColor = isSelected ? .red : .blue
        }
    }
    
    override init(frame: CGRect) {
        super.init(frame: frame)
        setupCell()
    }
    
    required init?(coder: NSCoder) {
        super.init(coder: coder)
        setupCell()
    }
    
    private func setupCell() {
        contentView.backgroundColor = .blue
        contentView.layer.cornerRadius = 8
        contentView.layer.masksToBounds = true
    }
}
```

### 示例代码

以下是一个完整的示例，展示了如何在单元格选中和取消选中时自动更新 UI。

#### 1. 创建自定义的 `UICollectionViewCell` 子类

```swift
import UIKit

class CustomCollectionViewCell: UICollectionViewCell {
    
    override var isSelected: Bool {
        didSet {
            contentView.backgroundColor = isSelected ? .red : .blue
        }
    }
    
    override init(frame: CGRect) {
        super.init(frame: frame)
        setupCell()
    }
    
    required init?(coder: NSCoder) {
        super.init(coder: coder)
        setupCell()
    }
    
    private func setupCell() {
        contentView.backgroundColor = .blue
        contentView.layer.cornerRadius = 8
        contentView.layer.masksToBounds = true
    }
}
```

#### 2. 在 `ViewController` 中使用自定义的单元格

```swift
import UIKit

class ViewController: UIViewController, UICollectionViewDataSource, UICollectionViewDelegate {
    
    var collectionView: UICollectionView!
    var items = Array(1...20)
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        // 创建布局
        let layout = UICollectionViewFlowLayout()
        layout.itemSize = CGSize(width: 100, height: 100)
        
        // 创建UICollectionView
        collectionView = UICollectionView(frame: self.view.frame, collectionViewLayout: layout)
        collectionView.backgroundColor = .white
        
        // 注册自定义cell
        collectionView.register(CustomCollectionViewCell.self, forCellWithReuseIdentifier: "CustomCell")
        
        // 设置数据源和代理
        collectionView.dataSource = self
        collectionView.delegate = self
        
        // 允许选择
        collectionView.allowsSelection = true
        // 如果需要多选，可以设置为true
        // collectionView.allowsMultipleSelection = true
        
        // 添加到视图
        self.view.addSubview(collectionView)
    }
    
    // UICollectionViewDataSource方法
    func collectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int {
        return items.count
    }
    
    func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
        let cell = collectionView.dequeueReusableCell(withReuseIdentifier: "CustomCell", for: indexPath) as! CustomCollectionViewCell
        return cell
    }
    
    // UICollectionViewDelegate方法
    func collectionView(_ collectionView: UICollectionView, didSelectItemAt indexPath: IndexPath) {
        print("Selected item at \(indexPath)")
    }
    
    func collectionView(_ collectionView: UICollectionView, didDeselectItemAt indexPath: IndexPath) {
        print("Deselected item at \(indexPath)")
    }
}
```

### 解释

1. **自定义单元格**：在 `CustomCollectionViewCell` 类中，重写了 `isSelected` 属性。当单元格的选中状态发生变化时，更新单元格的背景颜色。
2. **初始化单元格**：在 `setupCell` 方法中，设置单元格的初始外观。
3. **使用自定义单元格**：在 `ViewController` 中，注册并使用自定义的单元格。
4. **处理选中事件**：实现了 `collectionView(_:didSelectItemAt:)` 和 `collectionView(_:didDeselectItemAt:)` 方法来处理单元格的选中和取消选中事件。

通过这种方式，当你选中或取消选中一个单元格时，`UICollectionView` 会自动更新单元格的 UI，而不需要手动调用 `collectionView.reloadItems(at:)`。

---

# UItableView

## 自定义Cell

在 `UITableView` 中使用自定义的 `UITableViewCell` 可以让你更灵活地设计和展示表格中的内容。以下是如何创建和使用自定义 `UITableViewCell` 的详细步骤。

### 1. 创建自定义的 UITableViewCell 子类

首先，创建一个自定义的 `UITableViewCell` 子类。例如，我们创建一个名为 `CustomTableViewCell` 的类。

```swift
import UIKit

class CustomTableViewCell: UITableViewCell {
    
    // 自定义的 UI 元素
    let customLabel: UILabel = {
        let label = UILabel()
        label.translatesAutoresizingMaskIntoConstraints = false
        label.font = UIFont.systemFont(ofSize: 16)
        label.textColor = .black
        return label
    }()
    
    let customImageView: UIImageView = {
        let imageView = UIImageView()
        imageView.translatesAutoresizingMaskIntoConstraints = false
        imageView.contentMode = .scaleAspectFit
        return imageView
    }()
    
    // 初始化方法
    override init(style: UITableViewCell.CellStyle, reuseIdentifier: String?) {
        super.init(style: style, reuseIdentifier: reuseIdentifier)
        
        // 添加自定义的 UI 元素到 contentView
        contentView.addSubview(customLabel)
        contentView.addSubview(customImageView)
        
        // 设置约束
        NSLayoutConstraint.activate([
            customImageView.leadingAnchor.constraint(equalTo: contentView.leadingAnchor, constant: 10),
            customImageView.centerYAnchor.constraint(equalTo: contentView.centerYAnchor),
            customImageView.widthAnchor.constraint(equalToConstant: 40),
            customImageView.heightAnchor.constraint(equalToConstant: 40),
            
            customLabel.leadingAnchor.constraint(equalTo: customImageView.trailingAnchor, constant: 10),
            customLabel.trailingAnchor.constraint(equalTo: contentView.trailingAnchor, constant: -10),
            customLabel.centerYAnchor.constraint(equalTo: contentView.centerYAnchor)
        ])
    }
    
    // 这个初始化方法是必须实现的，用于从 storyboard 或 nib 文件中加载视图控制器
    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }
}
```

### 2. 在 ViewController 中注册和使用自定义的 UITableViewCell

在你的 `ViewController` 中，注册并使用自定义的 `UITableViewCell`。

```swift
import UIKit

class MyViewController: UIViewController, UITableViewDataSource, UITableViewDelegate {
    
    // 创建一个 UITableView 实例
    let tableView = UITableView()
    
    // 数据数组
    let data = ["Item 1", "Item 2", "Item 3", "Item 4", "Item 5"]

    override func viewDidLoad() {
        super.viewDidLoad()
        
        // 设置视图控制器的背景颜色
        view.backgroundColor = .white
        
        // 设置 tableView 的数据源和代理
        tableView.dataSource = self
        tableView.delegate = self
        
        // 注册自定义的 UITableViewCell
        tableView.register(CustomTableViewCell.self, forCellReuseIdentifier: "CustomCell")
        
        // 将 tableView 添加到视图控制器的视图中
        view.addSubview(tableView)
        
        // 设置 tableView 的约束
        tableView.translatesAutoresizingMaskIntoConstraints = false
        NSLayoutConstraint.activate([
            tableView.topAnchor.constraint(equalTo: view.topAnchor),
            tableView.bottomAnchor.constraint(equalTo: view.bottomAnchor),
            tableView.leadingAnchor.constraint(equalTo: view.leadingAnchor),
            tableView.trailingAnchor.constraint(equalTo: view.trailingAnchor)
        ])
    }
    
    // MARK: - UITableViewDataSource
    
    // 返回表格中行的数量
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return data.count
    }
    
    // 配置每一行的单元格
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "CustomCell", for: indexPath) as! CustomTableViewCell
        cell.customLabel.text = data[indexPath.row]
        cell.customImageView.image = UIImage(named: "exampleImage") // 替换为你的图片名称
        return cell
    }
    
    // MARK: - UITableViewDelegate
    
    // 处理行选择事件
    func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        tableView.deselectRow(at: indexPath, animated: true)
        print("Selected row at \(indexPath.row)")
    }
}
```

### 详细步骤解释

1. **创建自定义的 `UITableViewCell` 子类**：
   - 创建一个继承自 `UITableViewCell` 的子类 `CustomTableViewCell`。
   - 在该类中添加自定义的 UI 元素（如 `UILabel` 和 `UIImageView`）。
   - 在初始化方法中，将自定义的 UI 元素添加到 `contentView` 并设置它们的约束。

2. **在视图控制器中注册自定义的 `UITableViewCell`**：
   - 使用 `tableView.register(CustomTableViewCell.self, forCellReuseIdentifier: "CustomCell")` 注册自定义的单元格。

3. **在数据源方法中使用自定义的 `UITableViewCell`**：
   - 在 `tableView(_:cellForRowAt:)` 方法中，使用 `dequeueReusableCell(withIdentifier:for:)` 获取自定义的单元格实例，并配置其内容。

通过以上步骤，你可以在 `UITableView` 中使用自定义的单元格，从而更灵活地展示和管理表格中的数据。


---

# UICollectionView

在 Swift 中使用自定义的 `UICollectionViewCell` 作为 `UICollectionView` 的单元格需要几个步骤，包括创建自定义的 `UICollectionViewCell` 类、在 `UICollectionView` 中注册该类，以及在数据源方法中使用它。以下是详细的步骤：

### 1. 创建自定义的 `UICollectionViewCell` 类

首先，你需要创建一个自定义的 `UICollectionViewCell` 子类，并在其中定义你需要的 UI 元素。

```swift
import UIKit

class CustomCollectionViewCell: UICollectionViewCell {
    
    // 定义你需要的 UI 元素
    let label: UILabel = {
        let label = UILabel()
        label.translatesAutoresizingMaskIntoConstraints = false
        return label
    }()
    
    override init(frame: CGRect) {
        super.init(frame: frame)
        
        // 将 UI 元素添加到 cell 的 contentView
        contentView.addSubview(label)
        
        // 设置 UI 元素的约束
        NSLayoutConstraint.activate([
            label.centerXAnchor.constraint(equalTo: contentView.centerXAnchor),
            label.centerYAnchor.constraint(equalTo: contentView.centerYAnchor)
        ])
    }
    
    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }
}
```

### 2. 注册自定义的 `UICollectionViewCell` 类

在你的 `UIViewController` 或 `UICollectionViewController` 中注册自定义的 `UICollectionViewCell` 类。

```swift
import UIKit

class MyViewController: UIViewController, UICollectionViewDataSource, UICollectionViewDelegateFlowLayout {
    
    var collectionView: UICollectionView!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        // 创建 UICollectionViewFlowLayout
        let layout = UICollectionViewFlowLayout()
        
        // 创建 UICollectionView
        collectionView = UICollectionView(frame: self.view.bounds, collectionViewLayout: layout)
        collectionView.translatesAutoresizingMaskIntoConstraints = false
        collectionView.backgroundColor = .white
        
        // 注册自定义的 UICollectionViewCell 类
        collectionView.register(CustomCollectionViewCell.self, forCellWithReuseIdentifier: "CustomCell")
        
        // 设置数据源和代理
        collectionView.dataSource = self
        collectionView.delegate = self
        
        // 将 UICollectionView 添加到视图
        view.addSubview(collectionView)
        
        // 设置 UICollectionView 的约束
        NSLayoutConstraint.activate([
            collectionView.topAnchor.constraint(equalTo: view.topAnchor),
            collectionView.bottomAnchor.constraint(equalTo: view.bottomAnchor),
            collectionView.leadingAnchor.constraint(equalTo: view.leadingAnchor),
            collectionView.trailingAnchor.constraint(equalTo: view.trailingAnchor)
        ])
    }
    
    // UICollectionViewDataSource 方法
    func collectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int {
        return 20 // 返回单元格的数量
    }
    
    func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
        let cell = collectionView.dequeueReusableCell(withReuseIdentifier: "CustomCell", for: indexPath) as! CustomCollectionViewCell
        cell.label.text = "Item \(indexPath.row)"
        return cell
    }
    
    // UICollectionViewDelegateFlowLayout 方法
    func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, sizeForItemAt indexPath: IndexPath) -> CGSize {
        return CGSize(width: 100, height: 100) // 返回单元格的大小
    }
}
```

### 3. 运行应用

当你运行应用时，你会看到一个包含自定义单元格的 `UICollectionView`，每个单元格中都有一个标签，显示其索引。

### 总结

通过上述步骤，你可以在 Swift 中使用自定义的 `UICollectionViewCell` 作为 `UICollectionView` 的单元格。关键步骤包括创建自定义单元格类、在 `UICollectionView` 中注册该类，并在数据源方法中使用它。这样可以让你在 `UICollectionView` 中显示更复杂和定制化的内容。


**技巧**
UICollectionView有两种方式实现选中取消：
1. 重写cell的isSelected，在  **func** collectionView(_ collectionView: UICollectionView, didSelectItemAt indexPath: IndexPath)和 **func** collectionView(_ collectionView: UICollectionView, didDeselectItemAt indexPath: IndexPath)方法中进行更新UI操作
2. 在dataSource的Model中添加一个isSelected的属性，在视图初始化UI configure中进行UI渲染，设置点击事件为
```swift
    func collectionView(_ collectionView: UICollectionView, didSelectItemAt indexPath: IndexPath) {

        if let cell = collectionView.dequeueReusableCell(withReuseIdentifier: "CFOneClickChatCollectionViewCell", for: indexPath) as? CFOneClickChatCollectionViewCell {

            self.userList[indexPath.item].isSelectedUser.toggle()

            collectionView.reloadItems(at: [indexPath])

        }

    }
```

---



# layer

`ageLab.layer.masksToBounds = true` 是用于控制 `UILabel` 的图层（`layer`）是否裁剪其子图层的属性。具体来说，这个属性的作用如下：

### 作用

- **裁剪子图层**：当 `masksToBounds` 属性设置为 `true` 时，`ageLab` 的图层会裁剪掉超出其边界的所有子图层内容。也就是说，子图层的内容如果超出了 `ageLab` 的边界，那么超出的部分将不会被显示。

### 常见用途

1. **圆角效果**：
   当你为 `UILabel` 设置圆角时，需要将 `masksToBounds` 设置为 `true` 才能使圆角效果生效。

   ```swift
   ageLab.layer.cornerRadius = 10
   ageLab.layer.masksToBounds = true
   ```

   这里 `cornerRadius` 属性设置了圆角的半径，而 `masksToBounds = true` 确保了圆角之外的部分被裁剪掉，从而呈现出圆角效果。

2. **裁剪子视图**：
   当 `UILabel` 或其他视图有子视图时，设置 `masksToBounds = true` 可以确保子视图不会超出父视图的边界。

### 示例

假设你有一个 `UILabel`，并且希望它具有圆角效果：

```swift
let ageLab = UILabel()
ageLab.text = "Age: 25"
ageLab.backgroundColor = .lightGray
ageLab.textAlignment = .center

// 设置圆角
ageLab.layer.cornerRadius = 10
ageLab.layer.masksToBounds = true

// 设置其他属性
ageLab.frame = CGRect(x: 50, y: 50, width: 100, height: 40)
self.view.addSubview(ageLab)
```

在这个示例中：

- `ageLab.layer.cornerRadius = 10` 设置了圆角的半径。
- `ageLab.layer.masksToBounds = true` 确保了圆角之外的部分被裁剪掉，从而使圆角效果生效。

### 总结

`masksToBounds` 属性在视图需要裁剪其子视图或者应用圆角效果时非常有用。设置 `masksToBounds = true` 可以确保视图的内容和子视图不会超出其边界，从而实现预期的视觉效果。

---

# UIView的点击事件

UIImageView的isUserInterable默认为false

---

# UITableView

在 UIKit 中，`UITableView` 是一个复杂的视图组件，由多个子视图和相关的类构成。以下是 `UITableView` 的主要组成部分：

1. **UITableView**：这是表视图的主视图，负责管理和显示所有的行和部分。

2. **UITableViewCell**：表视图的每一行都是一个 `UITableViewCell` 对象。它是表视图的基本构建块，用户可以自定义单元格的内容和布局。

3. **UITableViewHeaderFooterView**：用于表视图的分区头部和尾部视图，可以自定义这些视图来显示分区的标题或其他信息。

4. **UITableViewSection**：虽然不是一个实际的视图，但表视图的数据是按分区组织的，每个分区包含若干行。每个分区可以有一个头部视图和一个尾部视图。

5. **UITableViewBackgroundView**：这是表视图的背景视图，可以设置为自定义的视图来改变表视图的背景。

6. **UITableViewIndex**：如果表视图有索引条（通常用于快速滚动到特定部分），这个索引条也是表视图的一部分。

### 具体的视图层次结构

在运行时，`UITableView` 的视图层次结构可能会更复杂。这是一个简化的视图层次结构示例：

```
UITableView
├── UITableViewWrapperView (私有视图，包装实际内容)
│   ├── UITableViewCell (每个单元格)
│   │   └── ContentView (单元格的内容视图)
│   ├── UITableViewHeaderFooterView (头部或尾部视图)
│   └── ...
├── UITableViewBackgroundView (背景视图)
└── UITableViewIndex (索引条，如果有的话)
```

### 详细解释

- **UITableView**：主视图，包含所有的子视图和内容。
- **UITableViewWrapperView**：这是一个私有视图，用于包装实际的内容视图。你通常不会直接与这个视图交互。
- **UITableViewCell**：每个单元格视图，包含一个内容视图（`contentView`），你可以在其中添加和布局自定义的子视图。
- **UITableViewHeaderFooterView**：用于显示分区的头部和尾部视图，可以自定义这些视图。
- **UITableViewBackgroundView**：表视图的背景视图，可以设置为自定义视图。
- **UITableViewIndex**：如果表视图有索引条（通常用于快速导航），这个索引条也是表视图的一部分。

### 使用示例

在实际使用中，你通常会自定义 `UITableViewCell` 和 `UITableViewHeaderFooterView`，并通过数据源和委托方法来管理表视图的内容和行为。例如：

```swift
class ViewController: UIViewController, UITableViewDataSource, UITableViewDelegate {
    
    let tableView = UITableView()
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        tableView.dataSource = self
        tableView.delegate = self
        tableView.register(UITableViewCell.self, forCellReuseIdentifier: "cell")
        
        view.addSubview(tableView)
        tableView.translatesAutoresizingMaskIntoConstraints = false
        NSLayoutConstraint.activate([
            tableView.topAnchor.constraint(equalTo: view.topAnchor),
            tableView.bottomAnchor.constraint(equalTo: view.bottomAnchor),
            tableView.leadingAnchor.constraint(equalTo: view.leadingAnchor),
            tableView.trailingAnchor.constraint(equalTo: view.trailingAnchor)
        ])
    }
    
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return 10
    }
    
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "cell", for: indexPath)
        cell.textLabel?.text = "Row \(indexPath.row)"
        return cell
    }
    
    func tableView(_ tableView: UITableView, heightForRowAt indexPath: IndexPath) -> CGFloat {
        return 50
    }
}
```

通过这种方式，你可以创建和管理一个 `UITableView` 及其子视图。


---

#  UIPageViewController

要创建一个包含两个按钮和两个子视图的 `ViewController`，并且可以通过按钮点击和左右滑动来切换视图，可以使用 `UIPageViewController` 来实现。以下是一个详细的步骤和示例代码。

### 步骤

1. **创建一个主视图控制器**，其中包含两个按钮和一个 `UIPageViewController`。
2. **配置 `UIPageViewController`**，使其包含两个子视图控制器。
3. **实现按钮点击事件**，以切换 `UIPageViewController` 中的视图。
4. **实现数据源方法**，以支持通过滑动来切换视图。

### 示例代码

#### 主视图控制器

```swift
import UIKit

class MainViewController: UIViewController, UIPageViewControllerDataSource, UIPageViewControllerDelegate {

    var pageViewController: UIPageViewController!
    var viewControllers: [UIViewController] = []
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        // 设置主视图背景颜色
        view.backgroundColor = .white
        
        // 创建两个子视图控制器
        let firstVC = UIViewController()
        firstVC.view.backgroundColor = .red
        let secondVC = UIViewController()
        secondVC.view.backgroundColor = .blue
        
        viewControllers = [firstVC, secondVC]
        
        // 创建 UIPageViewController
        pageViewController = UIPageViewController(transitionStyle: .scroll, navigationOrientation: .horizontal, options: nil)
        pageViewController.dataSource = self
        pageViewController.delegate = self
        
        // 设置初始视图控制器
        pageViewController.setViewControllers([firstVC], direction: .forward, animated: true, completion: nil)
        
        // 将 UIPageViewController 添加到主视图控制器中
        addChild(pageViewController)
        view.addSubview(pageViewController.view)
        pageViewController.didMove(toParent: self)
        
        // 设置 UIPageViewController 的布局
        pageViewController.view.translatesAutoresizingMaskIntoConstraints = false
        NSLayoutConstraint.activate([
            pageViewController.view.topAnchor.constraint(equalTo: view.topAnchor, constant: 100),
            pageViewController.view.leadingAnchor.constraint(equalTo: view.leadingAnchor),
            pageViewController.view.trailingAnchor.constraint(equalTo: view.trailingAnchor),
            pageViewController.view.bottomAnchor.constraint(equalTo: view.bottomAnchor)
        ])
        
        // 创建按钮
        let leftButton = UIButton(type: .system)
        leftButton.setTitle("左", for: .normal)
        leftButton.addTarget(self, action: #selector(leftButtonTapped), for: .touchUpInside)
        
        let rightButton = UIButton(type: .system)
        rightButton.setTitle("右", for: .normal)
        rightButton.addTarget(self, action: #selector(rightButtonTapped), for: .touchUpInside)
        
        // 添加按钮到视图
        view.addSubview(leftButton)
        view.addSubview(rightButton)
        
        // 设置按钮布局
        leftButton.translatesAutoresizingMaskIntoConstraints = false
        rightButton.translatesAutoresizingMaskIntoConstraints = false
        NSLayoutConstraint.activate([
            leftButton.leadingAnchor.constraint(equalTo: view.leadingAnchor, constant: 20),
            leftButton.topAnchor.constraint(equalTo: view.topAnchor, constant: 50),
            
            rightButton.trailingAnchor.constraint(equalTo: view.trailingAnchor, constant: -20),
            rightButton.topAnchor.constraint(equalTo: view.topAnchor, constant: 50)
        ])
    }
    
    // MARK: - 按钮点击事件
    
    @objc func leftButtonTapped() {
        if let currentViewController = pageViewController.viewControllers?.first,
           let currentIndex = viewControllers.firstIndex(of: currentViewController),
           currentIndex > 0 {
            let previousViewController = viewControllers[currentIndex - 1]
            pageViewController.setViewControllers([previousViewController], direction: .reverse, animated: true, completion: nil)
        }
    }
    
    @objc func rightButtonTapped() {
        if let currentViewController = pageViewController.viewControllers?.first,
           let currentIndex = viewControllers.firstIndex(of: currentViewController),
           currentIndex < viewControllers.count - 1 {
            let nextViewController = viewControllers[currentIndex + 1]
            pageViewController.setViewControllers([nextViewController], direction: .forward, animated: true, completion: nil)
        }
    }
    
    // MARK: - UIPageViewControllerDataSource
    
    func pageViewController(_ pageViewController: UIPageViewController, viewControllerBefore viewController: UIViewController) -> UIViewController? {
        guard let currentIndex = viewControllers.firstIndex(of: viewController), currentIndex > 0 else {
            return nil
        }
        return viewControllers[currentIndex - 1]
    }
    
    func pageViewController(_ pageViewController: UIPageViewController, viewControllerAfter viewController: UIViewController) -> UIViewController? {
        guard let currentIndex = viewControllers.firstIndex(of: viewController), currentIndex < viewControllers.count - 1 else {
            return nil
        }
        return viewControllers[currentIndex + 1]
    }
}
```

### 解释

1. **初始化视图控制器**：
   - 创建两个子视图控制器 `firstVC` 和 `secondVC`，并设置其背景颜色。
   - 将这两个子视图控制器添加到 `viewControllers` 数组中。

2. **创建 `UIPageViewController`**：
   - 初始化 `UIPageViewController`，设置其过渡样式为 `.scroll`，导航方向为 `.horizontal`。
   - 设置数据源和代理为当前视图控制器。
   - 设置初始视图控制器为 `firstVC`。

3. **布局 `UIPageViewController`**：
   - 将 `UIPageViewController` 添加到主视图控制器中，并设置其布局约束。

4. **创建并布局按钮**：
   - 创建两个按钮 `leftButton` 和 `rightButton`，并设置其点击事件。
   - 将按钮添加到视图中，并设置其布局约束。

5. **实现按钮点击事件**：
   - `leftButtonTapped` 和 `rightButtonTapped` 方法分别用于切换到前一个和后一个视图控制器。

6. **实现数据源方法**：
   - `pageViewController(_:viewControllerBefore:)` 和 `pageViewController(_:viewControllerAfter:)` 方法用于提供当前视图控制器之前和之后的视图控制器，以支持滑动切换视图。

这样，你就可以通过按钮点击和左右滑动来切换视图了。

---

# WebView

**设置`webView`为透明** 
```swift
// 设置背景颜色为透明 
webView.isOpaque = false 
webView.backgroundColor = .clear webView.scrollView.backgroundColor = .clear
```


---

# 下拉刷新

https://github.com/CoderMJLee/MJRefresh




---

# Font
初始化一个UILabel，如果不给字体大小
- **默认字体**：系统默认字体（通常是 San Francisco 字体）。
- **默认字体大小**：17.0 点（points）。
---
# UITextField

## 输入文本长度限制
```swift
    func textField(_ textField: UITextField, shouldChangeCharactersIn range: NSRange, replacementString string: String) -> Bool {

        let currentText = textField.text ?? ""

        guard let stringRange = Range(range, in: currentText) else { return false }

  

        let updatedText = currentText.replacingCharacters(in: stringRange, with: string)

        return updatedText.count <= 20

    }
```



---

# tintColor

[sarunw.com](https://sarunw.com/posts/tintcolor/)

## 什么是 tintColor？


tintColor 是 UIView 中返回颜色的变量。返回的颜色是接收器的 superview 链中的第一个非默认值（从自身开始）。如果未找到非默认值，则返回系统定义的颜色 （您始终看到的闪亮蓝色）。


## 介绍

 
许多系统 UI 使用此 tintColor 作为其主题机制，例如，系统 UIButton。

```swift
override func viewDidLoad() {    super.viewDidLoad()    let button = UIButton(type: .system)    button.setTitle("Default Button", for: .normal)    button.sizeToFit()    button.center = view.center    view.addSubview(button)}
```


上面的代码将生成一个色调为蓝色（系统定义颜色）的按钮。您可以在 iOS 系统中随处看到这种按钮和颜色。

![](https://cubox.pro/c/filters:no_upscale()?imageUrl=https%3A%2F%2Fsarunw.com%2Fimages%2Ftintcolor-default.png&valid=true)

Default UIButton 默认 UIButton

 
你可以通过将 `tintColor` 设置为视图控制器的视图来轻松更改应用程序的外观。

```swift
override func viewDidLoad() {    super.viewDidLoad()    let button = UIButton(type: .system)    button.setTitle("Default Button", for: .normal)    button.sizeToFit()    button.center = view.center    view.addSubview(button)    view.tintColor = .systemPink}
```

![](https://cubox.pro/c/filters:no_upscale()?imageUrl=https%3A%2F%2Fsarunw.com%2Fimages%2Ftintcolor-pink.png&valid=true)


上级视图的 tintColor 设置为 pink 的 UIButton

每个没有设置 tintColor 的按钮都将从此颜色中受益。

![](https://cubox.pro/c/filters:no_upscale()?imageUrl=https%3A%2F%2Fsarunw.com%2Fimages%2Ftintcolor-two-buttons.png&valid=true)


每个按钮都从其上级视图中获取 tintColor

 
我们可以通过在所需视图中设置 `tintColor` 来覆盖此颜色。在本例中，我们将第二个按钮色调颜色设置为 indigo。

```swift
let button = UIButton(type: .system)button.setTitle("Button 1", for: .normal)button.sizeToFit()button.center = view.centerstackView.addArrangedSubview(button)let button2 = UIButton(type: .system)button2.setTitle("Indigo", for: .normal)button2.sizeToFit()button2.center = view.centerbutton2.tintColor = .systemIndigostackView.addArrangedSubview(button2)view.tintColor = .systemPink
```

![](https://cubox.pro/c/filters:no_upscale()?imageUrl=https%3A%2F%2Fsarunw.com%2Fimages%2Ftintcolor-indigo.png&valid=true)

Override tint color 覆盖色调颜色

## Global tintColor  全局 tintColor

If you use a storyboard, open a storyboard, and select the File inspector tab. Then select a color of your choice in a **Global Tint** field.  
如果使用 Storyboard，请打开 Storyboard，然后选择 File inspector 选项卡。然后在 **Global Tint （全局色调**） 字段中选择您选择的颜色。

### Storyboard  脚本

If you use storyboard, open the storyboard, and select File inspector tab. Then select a color of your choice in a **Global Tint** field.  
如果使用 Storyboard，请打开 Storyboard，然后选择 File inspector（文件检查器）选项卡。然后在 **Global Tint （全局色调**） 字段中选择您选择的颜色。

![](https://cubox.pro/c/filters:no_upscale()?imageUrl=https%3A%2F%2Fsarunw.com%2Fimages%2Ftintcolor-global.png&valid=true)

The Global Tint property in the storyboard's File inspector  
故事板的 File Inspector 中的 Global Tint 属性

If you have many storyboards or not use storyboards at all, this way of setting tint color might not work for you. Luckily there is another way to do it.  
如果您有许多 Storyboard 或根本不使用 Storyboard，则这种设置色调颜色的方法可能不适合您。幸运的是，还有另一种方法可以做到这一点。

### Window  窗

As I mentioned before, tint color is inherited from an ancestor, so you can apply the same tint color for every view by set tintColor to an ancestor of all views, UIWindow (UIWindow is a subclass of UIView).  
如前所述，色调颜色是从祖先继承的，因此您可以通过将 tintColor 设置为所有视图的祖先 UIWindow（UIWindow 是 UIView 的子类）来为每个视图应用相同的色调颜色。

Remove `view.tintColor = .systemPink` from the view controller, then set `tintColor` to `UIWindow`.  
从视图控制器中删除 `view.tintColor = .systemPink`，然后将 `tintColor` 设置为 `UIWindow`。

```
window?.tintColor = .systemGreen
```

Setting color to UIWindow would apply the color everywhere.  
将 color 设置为 UIWindow 会将颜色应用于所有位置。

![](https://cubox.pro/c/filters:no_upscale()?imageUrl=https%3A%2F%2Fsarunw.com%2Fimages%2Ftintcolor-window.png&valid=true)

Apply tint color to UIWindow  
将色调应用于 UIWindow

## Custom View  自定义视图

We use a button as an example throughout the article, but you can have your custom view benefit from this tint color.  
我们在整篇文章中使用一个按钮作为示例，但您可以让您的自定义视图从这种色调中受益。

Let's start by creating a custom view. I create a square view with a tint color background.  
让我们从创建自定义视图开始。我创建了一个具有色调背景的方形视图。

```
class MyCustomView: UIView {    override init(frame: CGRect) {        super.init(frame: frame)        backgroundColor = tintColor    }    required init?(coder: NSCoder) {        super.init(coder: coder)    }    override func awakeFromNib() {        super.awakeFromNib()        backgroundColor = tintColor    }    override var intrinsicContentSize: CGSize {        return CGSize(width: 50, height: 50)    }}
```

Add it to the view controller and run.  
将其添加到视图控制器并运行。

![](https://cubox.pro/c/filters:no_upscale()?imageUrl=https%3A%2F%2Fsarunw.com%2Fimages%2Ftintcolor-custom-1.png&valid=true)

Custom view 自定义视图

The result might not be the one we expected. Our custom view gets default background color. The reason is at the time that the custom view gets created, it didn't add to any view, so the tint color is the default one at that time.  
结果可能不是我们预期的。我们的自定义视图获得默认背景颜色。原因是在创建自定义视图时，它没有添加到任何视图，因此色调是当时的默认颜色。

To make a custom view listen for the tint color changes, you need to override `tintColorDidChange()`method. The implementation is straightforward, you refresh the view using the new tint color.  
要使自定义视图侦听色调颜色更改，您需要覆盖 `tintColorDidChange（）` 方法。实现非常简单，您可以使用新的色调颜色刷新视图。

```
override func tintColorDidChange() {    super.tintColorDidChange()    backgroundColor = tintColor}
```

Run it again, and the result is perfect.  
再次运行它，结果是完美的。

![](https://cubox.pro/c/filters:no_upscale()?imageUrl=https%3A%2F%2Fsarunw.com%2Fimages%2Ftintcolor-custom-2.png&valid=true)

Custom view 自定义视图

## Conclusion  结论

tintColor is an essential part of theming in of iOS system. That's why it is a property in every view. Even a UIBarButtonItem, which is not a view, still have this tintColor property. Get to know this property might help you sometime in the future.  
tintColor 是 iOS 系统主题化的重要组成部分。这就是为什么它在每个视图中都是一个属性。即使是不是视图的 UIBarButtonItem 也仍然具有此 tintColor 属性。了解此属性可能会在将来的某个时候对您有所帮助。

![](https://cubox.pro/c/filters:no_upscale()?imageUrl=https%3A%2F%2Fsarunw.com%2Fimages%2Ftintcolor-barbuttonitem.png&valid=true)

UIBarButtonItem also has tintColor  
UIBarButtonItem 也具有 tintColor

## Related Resources  相关资源

[Apple Documentation – UIView – tintColor  
Apple 文档 – UIView – tintColor](https://developer.apple.com/documentation/uikit/uiview/1622467-tintcolor)  
[Apple Documentation – UIBarButtonItem – tintColor  
Apple 文档 – UIBarButtonItem – tintColor](https://developer.apple.com/documentation/uikit/uibarbuttonitem/1617135-tintcolor)

[sarunw.com](https://sarunw.com/posts/tintcolor/)

---


# UIkit将一个VC充满其父视图

在UIKit中，你可以使用Auto Layout约束来让一个视图充满其父视图。以下是如何在Swift中实现这个功能的代码：

```swift
let childViewController = YourViewController()
addChild(childViewController)
view.addSubview(childViewController.view)
childViewController.didMove(toParent: self)

childViewController.view.translatesAutoresizingMaskIntoConstraints = false
NSLayoutConstraint.activate([
    childViewController.view.leadingAnchor.constraint(equalTo: view.leadingAnchor),
    childViewController.view.trailingAnchor.constraint(equalTo: view.trailingAnchor),
    childViewController.view.topAnchor.constraint(equalTo: view.topAnchor),
    childViewController.view.bottomAnchor.constraint(equalTo: view.bottomAnchor)
])
```

这段代码首先创建了一个新的视图控制器，并将其添加为当前视图控制器的子视图控制器。然后，它将新的视图控制器的视图添加到当前视图控制器的视图中。

接下来，它禁用了新的视图控制器视图的自动尺寸调整，这是因为我们将使用Auto Layout约束来定义视图的位置和大小。

最后，它创建了四个约束，这些约束将新的视图控制器的视图的边缘与当前视图控制器的视图的相应边缘对齐。这样，新的视图控制器的视图就会充满其父视图。

请注意，你需要将`YourViewController`替换为你实际的视图控制器类名。

## UIView充满父视图

在UIKit中，你可以使用Auto Layout约束来让一个UIView充满其父视图。以下是如何在Swift中实现这个功能的代码：

```swift
let childView = UIView()
parentView.addSubview(childView)

childView.translatesAutoresizingMaskIntoConstraints = false
NSLayoutConstraint.activate([
    childView.leadingAnchor.constraint(equalTo: parentView.leadingAnchor),
    childView.trailingAnchor.constraint(equalTo: parentView.trailingAnchor),
    childView.topAnchor.constraint(equalTo: parentView.topAnchor),
    childView.bottomAnchor.constraint(equalTo: parentView.bottomAnchor)
])
```

这段代码首先创建了一个新的UIView，并将其添加到父视图中。

然后，它禁用了新的UIView的自动尺寸调整，这是因为我们将使用Auto Layout约束来定义视图的位置和大小。

最后，它创建了四个约束，这些约束将新的UIView的边缘与父视图的相应边缘对齐。这样，新的UIView就会充满其父视图。

请注意，你需要将`parentView`替换为你实际的父视图变量名。

---
