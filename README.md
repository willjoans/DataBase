# DataBase


import RealmSwift
import Realm

        IQKeyboardManager.shared.enable = true
        print(Realm.Configuration.defaultConfiguration.fileURL!)


MOdel:-
import UIKit
import RealmSwift
class AlertBean: Object {
    
    @objc dynamic var AlertID :Int = 0
    @objc dynamic var Description :String = ""
    @objc dynamic var Date :String = ""
    @objc dynamic var Time :String = ""
    @objc dynamic var Repeter :String = ""
    @objc dynamic var Favorite : Bool = false
    @objc dynamic var IselecteFlage : Int = 0
   
    
    override static func primaryKey() -> String? {
        return "AlertID"
    }
    override static func indexedProperties() -> [String] {
        return ["AlertID"]
    }
    func incrementID() -> Int {
        let realm = try! Realm()
        return (realm.objects(AlertBean.self).max(ofProperty: "AlertID") as Int? ?? 0) + 1
    }
}


///INsert Update,Delete
func UpdateDataInsert(){
        let realm = try? Realm()
        do {
            let Bean = AlertBean()
            Bean.AlertID = Bean.incrementID()
            Bean.Description = txtCleint.text!
            Bean.Date = txtDate.text!
            Bean.Time = txtTime.text!
            Bean.Repeter = txtRepeat.text!
            Bean.Favorite = false
            Bean.IselecteFlage = 0
            try! realm?.write {
                realm?.add(Bean)
                
                appDelegate.window?.rootViewController?.view.makeToast(message: "\(String(describing: "Sucessfully Added Insert."))")
                self.navigationController?.popViewController(animated: true)
                print(Bean)
            }
            
        }
        catch let error {
            print(".........Error in add User function.........")
            print(error.localizedDescription)
        }
    }
    func Data_Update_Add(){
        let realm = try? Realm()
        do {
            let Bean = AlertBean()
            Bean.AlertID = BeanDetaile.AlertID
            Bean.Description = txtCleint.text!
            Bean.Date = txtDate.text!
            Bean.Time = txtTime.text!
            Bean.Repeter = txtRepeat.text!
            Bean.Favorite = BeanDetaile.Favorite
            Bean.IselecteFlage = BeanDetaile.IselecteFlage
            try! realm?.write {
                realm?.add(Bean, update: true)
                appDelegate.window?.rootViewController?.view.makeToast(message: "\(String(describing: "Sucessfully Update."))")
                self.navigationController?.popViewController(animated: true)
                print(Bean)
            }
            
        }
        catch let error {
            print(".........Error in add User function.........")
            print(error.localizedDescription)
        }
        
    }
    //Delete
    let refreshAlert = UIAlertController(title: "CalendarDemo", message: "are you sure want to delete Today Data", preferredStyle: UIAlertController.Style.alert)
        
        refreshAlert.addAction(UIAlertAction(title: "YES", style: .destructive, handler: { (action: UIAlertAction!) in
            
            if let item = self.ArrayForClientData?[sender.tag] {
                try! self.realm.write {
                    self.realm.delete(item)
                   
                }
                if self.ArrayForClientData?.count == 0{
                    self.lblDatanotToday.isHidden = false
                }else{
                    self.lblDatanotToday.isHidden = true
                }
                self.tblviewTodays.reloadData()
            }
            
        }))
        
        refreshAlert.addAction(UIAlertAction(title: "NO", style: .default, handler: { (action: UIAlertAction!) in
            refreshAlert .dismiss(animated: true, completion: nil)
        }))
        
        present(refreshAlert, animated: true, completion: nil)
        
        
        ///Get Array Data 
         ArrayFoavirite = realm.objects(AlertBean.self).filter("Favorite == %@",true)
        if ArrayFoavirite?.count == 0{
            self.lblDataNotFavorite.isHidden = false
        }else{
            self.lblDataNotFavorite.isHidden = true
        }
         self.tblviewTodays.reloadData()
         
         
         
         ///LOcal NOtification
         
         
         
         
         
