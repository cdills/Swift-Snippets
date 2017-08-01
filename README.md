
# Swift Snippets

### Get device height & width

    let screenRect = UIScreen.main.bounds
    let screenHeight = screenRect.size.height
    let screenWidth = screenRect.size.width


### Reposition admob frame to bottom of any device

    var bannerView: GADBannerView!
    var bannerDisplayed = false
    let screenRect = UIScreen.main.bounds

	viewdidload(){
   		adViewDidReceiveAd(view: bannerView)
	}

    func adViewDidReceiveAd(view: GADBannerView) {
        print("adViewDidReceiveAd:\(view)");
        bannerDisplayed = true
        relayoutViews()
    }
    
    func relayoutViews() {
        if (bannerDisplayed) {
            let screenHeight = screenRect.size.height
            var bannerFrame = bannerView!.frame
            bannerFrame.origin.x = 0
            bannerFrame.origin.y = screenHeight - bannerFrame.size.height
            bannerView!.frame = bannerFrame
        }
    }


### Force hide status bar. Place in view controller. Use with plist setting

    override var prefersStatusBarHidden: Bool { 
        return true
    }


### UI Alert with Text Field Template & numberpad

    Import UIkit
       let alert = UIAlertController(title: "", message: "", preferredStyle: .alert)
            alert.addTextField { (textField) in
                textField.keyboardType = UIKeyboardType.numberPad
                textField.text = ""
            }

            alert.addAction(UIAlertAction(title: "OK", style: .default, handler: { [weak alert] (_) in
                let textField = alert?.textFields![0]
                self.label.text = "\(textField?.text ?? "")"
            }))

            self.present(alert, animated: true, completion: nil)

### Create JSON object with “data” type input

    if let json = try JSONSerialization.jsonObject(with: data, options: .mutableContainers) as? [String: Any] {
                    print(json)



### Pull to refresh tableview with async queue

    func reloader() {
            DispatchQueue.main.async {
                self.tableView.reloadData()
                self.refresher.endRefreshing()
            }
        }

        override func viewDidLoad() {
            super.viewDidLoad()

            //Implement resfresh control
            if #available(iOS 10.0, *) {
                tableView.refreshControl = refresher
            } else {
                tableView.addSubview(refresher)
            }

            refresher.addTarget(self, action: #selector(reloader), for: .valueChanged)
