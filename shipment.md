TABLE NAME shipment_services

    id INT UNSIGNED
    order_id INT UNSIGNED
    user_id INT UNSIGNED
    service_name VARCHAR(100)
    status - ( requested, approved ) DEFAULT "requested"
    response TEXT
    created_at DATETIME
    update_at DATETIME


# Library to user.
    1. Guzzle

