#Rizk PHP assessment
##1
You are handled a project which uses SQL, Redis and PHP.
The users are stored in table "User" in SQL and there is basic PHP class User.

Now the users are given items, which can be of 4 types:
1. 5 free spins
2. 10 free spins
3. 5 euros
4. 1 Raffle ticket

In the future there will be more item types.

1) design the SQL for saving items
2) design API to add and remove items from users
3) implement function exchange() in PHP which exchanges 5 free spins to 5 euros or vice versa
4) How would you utilize Redis for caching?

##2
The public route rizk.com/spin/{wheelId} is executed in the function spinAction. The parameter wheelId is passed from uri as a raw string to the function.
The route is called by client browser when a user spins his wheel of rizk.
What problems do you find in the following design and implementation? 

class User {
    $id;  // stored to session
    public funtion getWheel($wheelId) {
        $sql = "SELECT * FROM User_wheels where wheelId = $wheelId";
        $result = $pdo->query($sql)->fetch();
        return $result;
    }
}

public function getUser() {
    if ($loggedIn) return null;
    else return $session->getUser();
}

public function rewardWheelToUser($user, $wheel) {
    $sql = "DELETE * FROM User_wheels WHERE wheelId = $wheel->id";
    $result = $this->db->query($sql);

    $sql ="INSERT INTO User_rewards (userId, reward) values ($user->id, $wheel->reward)";
    $result = $this->db->query($sql);
    return $result;
}

public function spinAction($wheelId)
{
    $user = getUser();
    $wheel = $user->getWheel($wheelId);
    $success = rewardWheelToUser($user, $wheel);

    return json(['success' => $success]);
}
