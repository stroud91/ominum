# ominum

![image](https://github.com/user-attachments/assets/21061aa5-9fba-49a6-9ad8-80d0da0ee9cc)


Table users {
  id UUID [pk, not null]
  username VARCHAR(255) [unique, not null]
  email VARCHAR(255) [unique, not null]
  password_hash VARCHAR(255) [not null]
  role VARCHAR(50) [default: 'guest']
  created_at TIMESTAMP
  updated_at TIMESTAMP
  phone_number VARCHAR(20)
  is_verified BOOLEAN [default: false]
}

Table tours {
  id UUID [pk, not null]
  tour_name VARCHAR(255) [not null]
  description TEXT [not null]
  price DECIMAL(10, 2) [not null]
  start_date TIMESTAMP [not null]
  end_date TIMESTAMP [not null]
  created_by UUID [not null, ref: > users.id]
  created_at TIMESTAMP
  updated_at TIMESTAMP
  location VARCHAR(255) [not null]
  is_available BOOLEAN [default: true]
}

Table hotels {
  id UUID [pk, not null]
  hotel_name VARCHAR(255) [not null]
  address VARCHAR(255) [not null]
  price_per_night DECIMAL(10, 2) [not null]
  total_rooms INT [not null]
  available_rooms INT [not null]
  created_at TIMESTAMP
  updated_at TIMESTAMP
  city VARCHAR(255) [not null]
  contact_email VARCHAR(255)
}

Table car_rentals {
  id UUID [pk, not null]
  car_model VARCHAR(255) [not null]
  car_type VARCHAR(50) [not null]
  price_per_day DECIMAL(10, 2) [not null]
  availability_status VARCHAR(50) [default: 'available']
  created_at TIMESTAMP
  updated_at TIMESTAMP
  rental_company VARCHAR(255) [not null]
  location VARCHAR(255) [not null]
}

Table bookings {
  id UUID [pk, not null]
  user_id UUID [not null, ref: > users.id]
  booking_type VARCHAR(50) [not null]
  tour_id UUID [ref: > tours.id]
  hotel_id UUID [ref: > hotels.id]
  car_id UUID [ref: > car_rentals.id]
  start_date TIMESTAMP [not null]
  end_date TIMESTAMP [not null]
  total_cost DECIMAL(10, 2) [not null]
  created_at TIMESTAMP
  status VARCHAR(50) [default: 'pending']
}

Table payments {
  id UUID [pk, not null]
  booking_id UUID [not null, ref: > bookings.id]
  amount DECIMAL(10, 2) [not null]
  payment_date TIMESTAMP
  payment_status VARCHAR(50) [not null]
  payment_method VARCHAR(50) [not null]
}

Table reviews {
  id UUID [pk, not null]
  user_id UUID [not null, ref: > users.id]
  entity_type VARCHAR(50) [not null]
  entity_id UUID [not null]
  rating INT [not null]
  review_text TEXT
  created_at TIMESTAMP
  updated_at TIMESTAMP
}

Table admin_dashboard_activity_logs {
  id UUID [pk, not null]
  admin_id UUID [not null, ref: > users.id]
  action_type VARCHAR(50) [not null]
  entity_type VARCHAR(50) [not null]
  entity_id UUID
  timestamp TIMESTAMP
  details TEXT
}

Table tour_schedules {
  id UUID [pk, not null]
  tour_id UUID [not null, ref: > tours.id]
  day TIMESTAMP [not null]
  activities JSON
  created_at TIMESTAMP
  updated_at TIMESTAMP
}
