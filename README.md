# user-class
Php User class handler

```php
class Admin extends  \Peterujah\NanoBlock\User{
    const GUEST = "_admin_guest_class_";
    const LIVE = "_admin_live_class_";
    public function __construct($db){
        $this->db = $db;
        $this->index = "index";
        $this->setUserQuery("
            SELECT *
            FROM admin 
            WHERE admin_id = :check_user_key
            LIMIT 1
        ");
    }

    public function setLastLogin($ip){
        $this->conn()->prepare("
            UPDATE admin
            SET admin_last_login_date = NOW(),
                admin_last_login_ip = :admin_last_login_ip  
            WHERE admin_id = :admin_id
            LIMIT 1
        ");
        $this->conn()->bind(":admin_last_login_ip", $ip);
        $this->conn()->bind(":admin_id", $this->id());
        $this->conn()->execute();		
        $this->conn()->free();
        return $this;
    }
}
```
