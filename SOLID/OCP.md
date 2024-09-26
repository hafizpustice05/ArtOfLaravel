<!-- TABLE OF CONTENTS -->

## Art Of OOP

- [Initial Implementation Violating OCP](#Initial-Implementation-Violating-OCP)
  - [Refactored Implementation](#Refactored-Implementation)
  - [Define an Interface](#Define-an-Interface)
  - [Implement Concrete Classes](#Implement-Concrete-Classes)
  - [Refactor the NotificationService Class](#Refactor-the-NotificationService-Class)
  - [Adding a New Notification Type](#Adding-a-New-Notification-Type)
- [Contact](#contact)

  <!-- UPDATE NODE -->

## Initial Implementation (Violating OCP)

In a naive implementation, you might have a NotificationService class that handles sending notifications, but each notification type is hardcoded within this class.

```php
class NotificationService {
    public function sendNotification($type, $message) {
        if ($type === 'email') {
            $this->sendEmail($message);
        } elseif ($type === 'sms') {
            $this->sendSMS($message);
        }
        // If we want to add more notification types, we'd modify this class.
    }
    private function sendEmail($message) {
        // to do something
    }
    private function sendSMS($message) {
        // to do something
    }
}
```

## Refactored Implementation (Following OCP)

To adhere to the Open/Closed Principle, you can refactor the code by introducing an interface and separate classes for each notification type:

### Step 1: Define an Interface

Create an interface that defines a send method.

```php
interface Notification {
    public function send($message);
}
```

### Step 2: Implement Concrete Classes

Create concrete classes for each notification type that implements the `Notification` interface.

```php
class EmailNotification implements Notification {
    public function send($message) {
        echo "Sending email: $message\n";
    }
}

class SMSNotification implements Notification {
    public function send($message) {
        echo "Sending SMS: $message\n";
    }
}

```

### Step 3: Refactor the NotificationService Class

Now, the `NotificationService` class will depend on the `Notification` interface rather than specific implementations.

```php
class NotificationService {
    private $notification;

    public function __construct(Notification $notification) {
        $this->notification = $notification;
    }

    public function sendNotification($message) {
        $this->notification->send($message);
    }
}
```

`Usage`

Now you can easily add new notification types without modifying existing code:

```php
/*
* Sending email: Hello via Email!
*/
$service1 = (new NotificationService(new EmailNotification()))->sendNotification('Hello via Email!');

/*
* Sending SMS: Hello via SMS!
*/
$service2 = (new NotificationService(new SMSNotification()))->sendNotification('Hello via SMS!');

```

### Adding a New Notification Type

If you want to add a new type of notification, such as a `PushNotification`, you simply create a new class without altering the existing classes.

```php
class PushNotification implements Notification {
    public function send($message) {
        echo "Sending push notification: $message\n";
    }
}

/*
* Usage
* Sending push notification: Hello via Push!
*/
$service3 = (new NotificationService(new PushNotification()))->sendNotification('Hello via Push!');

```

## Summary

In this example, we:

- Defined a `Notification` interface that allows different types of notifications to be sent.
- Created concrete classes for each notification type (Email, SMS, Push, etc.) implementing the interface.
- Modified the `NotificationService` class to depend on the `Notification` interface, allowing it to work with any notification type.

This design adheres to the Open/Closed Principle, as we can extend the functionality (add new notification types) without modifying the existing `NotificationService` or other classes. It enhances maintainability, flexibility, and readability of the code.

## Contact

Md Hafizul Islam - [hafizpustice05@gmail.com](mailto:hafizpustice05@gmail.com)
