# 🚗 EzPark - API Gateway Routes Documentation

## 📋 **Configuración del Gateway**

**Puerto:** `8080`  
**Servicio:** `api-gateway`  
**Eureka Discovery:** `http://discovery-server:8761/eureka/`

---

## 🛣️ **Rutas de Microservicios**

### 🔐 **IAM Service (Autenticación)**
| Cliente Solicita | Gateway Reenvía | Microservicio Destino |
|------------------|-----------------|----------------------|
| `GET /api/auth/authentication/sign-in` | `GET /api/v1/authentication/sign-in` | `iam-service:8081` |
| `POST /api/auth/authentication/sign-up` | `POST /api/v1/authentication/sign-up` | `iam-service:8081` |
| `GET /api/auth/roles` | `GET /api/v1/roles` | `iam-service:8081` |
| `GET /api/auth/users` | `GET /api/v1/users` | `iam-service:8081` |

**Configuración:**
```properties
spring.cloud.gateway.routes[0].predicates[0]=Path=/api/auth/**
spring.cloud.gateway.routes[0].filters[0]=RewritePath=/api/auth/(?<remaining>.*), /api/v1/${remaining}
```

---

### 👤 **Profile Service**
| Cliente Solicita | Gateway Reenvía | Microservicio Destino |
|------------------|-----------------|----------------------|
| `GET /api/profiles` | `GET /api/v1/profiles` | `profile-service:8082` |
| `GET /api/profiles/{id}` | `GET /api/v1/profiles/{id}` | `profile-service:8082` |
| `POST /api/profiles` | `POST /api/v1/profiles` | `profile-service:8082` |
| `PUT /api/profiles/{id}` | `PUT /api/v1/profiles/{id}` | `profile-service:8082` |
| `DELETE /api/profiles/delete/{id}` | `DELETE /api/v1/profiles/delete/{id}` | `profile-service:8082` |

**Configuración:**
```properties
spring.cloud.gateway.routes[1].predicates[0]=Path=/api/profiles/**
spring.cloud.gateway.routes[1].filters[0]=RewritePath=/api/profiles(?<remaining>.*), /api/v1/profiles${remaining}
```

---

### 🚗 **Vehicle Service**
| Cliente Solicita | Gateway Reenvía | Microservicio Destino |
|------------------|-----------------|----------------------|
| `GET /api/vehicles-management/vehicles` | `GET /api/v1/vehicles` | `vehicle-service:8083` |
| `GET /api/vehicles-management/vehicles/{id}` | `GET /api/v1/vehicles/{id}` | `vehicle-service:8083` |
| `GET /api/vehicles-management/vehicles/profile/{id}` | `GET /api/v1/vehicles/profile/{id}` | `vehicle-service:8083` |
| `POST /api/vehicles-management/vehicles` | `POST /api/v1/vehicles` | `vehicle-service:8083` |
| `PUT /api/vehicles-management/vehicles/{id}` | `PUT /api/v1/vehicles/{id}` | `vehicle-service:8083` |
| `DELETE /api/vehicles-management/vehicles/{id}` | `DELETE /api/v1/vehicles/{id}` | `vehicle-service:8083` |

**Configuración:**
```properties
spring.cloud.gateway.routes[2].predicates[0]=Path=/api/vehicles-management/**
spring.cloud.gateway.routes[2].filters[0]=RewritePath=/api/vehicles-management/(?<remaining>.*), /api/v1/${remaining}
```

---

### 🅿️ **Parking Service**
| Cliente Solicita | Gateway Reenvía | Microservicio Destino |
|------------------|-----------------|----------------------|
| **Parking Endpoints** |
| `GET /api/parking-management/parking` | `GET /api/v1/parking` | `parking-service:8084` |
| `POST /api/parking-management/parking` | `POST /api/v1/parking` | `parking-service:8084` |
| `PUT /api/parking-management/parking/{id}` | `PUT /api/v1/parking/{id}` | `parking-service:8084` |
| `DELETE /api/parking-management/parking/{id}` | `DELETE /api/v1/parking/{id}` | `parking-service:8084` |
| `GET /api/parking-management/parking/{id}/details` | `GET /api/v1/parking/{id}/details` | `parking-service:8084` |
| `GET /api/parking-management/parking/profile/{id}` | `GET /api/v1/parking/profile/{id}` | `parking-service:8084` |
| `GET /api/parking-management/parking/nearby?lat={lat}&lng={lng}` | `GET /api/v1/parking/nearby?lat={lat}&lng={lng}` | `parking-service:8084` |
| **Location Endpoints** |
| `GET /api/parking-management/location` | `GET /api/v1/location` | `parking-service:8084` |
| `PUT /api/parking-management/location/{id}` | `PUT /api/v1/location/{id}` | `parking-service:8084` |
| **Schedule Endpoints** |
| `GET /api/parking-management/schedule` | `GET /api/v1/schedule` | `parking-service:8084` |
| `GET /api/parking-management/schedule/{id}` | `GET /api/v1/schedule/{id}` | `parking-service:8084` |
| `POST /api/parking-management/schedule` | `POST /api/v1/schedule` | `parking-service:8084` |
| `PUT /api/parking-management/schedule/{id}` | `PUT /api/v1/schedule/{id}` | `parking-service:8084` |
| `DELETE /api/parking-management/schedule/{id}` | `DELETE /api/v1/schedule/{id}` | `parking-service:8084` |

**Configuración:**
```properties
spring.cloud.gateway.routes[3].predicates[0]=Path=/api/parking-management/**
spring.cloud.gateway.routes[3].filters[0]=RewritePath=/api/parking-management/(?<remaining>.*), /api/v1/${remaining}
```

---

### 📅 **Reservation Service**
| Cliente Solicita | Gateway Reenvía | Microservicio Destino |
|------------------|-----------------|----------------------|
| `GET /api/reservations` | `GET /api/v1/reservations` | `reservation-service:8085` |
| `GET /api/reservations/{id}` | `GET /api/v1/reservations/{id}` | `reservation-service:8085` |
| `POST /api/reservations` | `POST /api/v1/reservations` | `reservation-service:8085` |
| `PUT /api/reservations/{id}` | `PUT /api/v1/reservations/{id}` | `reservation-service:8085` |
| `PUT /api/reservations/{id}/status` | `PUT /api/v1/reservations/{id}/status` | `reservation-service:8085` |
| `GET /api/reservations/host/{hostId}` | `GET /api/v1/reservations/host/{hostId}` | `reservation-service:8085` |
| `GET /api/reservations/guest/{guestId}` | `GET /api/v1/reservations/guest/{guestId}` | `reservation-service:8085` |
| `GET /api/reservations/inProgress` | `GET /api/v1/reservations/inProgress` | `reservation-service:8085` |
| `GET /api/reservations/upComing` | `GET /api/v1/reservations/upComing` | `reservation-service:8085` |
| `GET /api/reservations/past` | `GET /api/v1/reservations/past` | `reservation-service:8085` |

**Configuración:**
```properties
spring.cloud.gateway.routes[4].predicates[0]=Path=/api/reservations/**
spring.cloud.gateway.routes[4].filters[0]=RewritePath=/api/reservations(?<remaining>.*), /api/v1/reservations${remaining}
```

---

### 💳 **Payment Service**
| Cliente Solicita | Gateway Reenvía | Microservicio Destino |
|------------------|-----------------|----------------------|
| `GET /api/payments` | `GET /api/v1/payments` | `payment-service:8086` |
| `GET /api/payments?reservationId={id}` | `GET /api/v1/payments?reservationId={id}` | `payment-service:8086` |
| `POST /api/payments` | `POST /api/v1/payments` | `payment-service:8086` |

**Configuración:**
```properties
spring.cloud.gateway.routes[5].predicates[0]=Path=/api/payments/**
spring.cloud.gateway.routes[5].filters[0]=RewritePath=/api/payments(?<remaining>.*), /api/v1/payments${remaining}
```

---

## 🌐 **Configuración CORS**

```properties
spring.cloud.gateway.globalcors.cors-configurations.[/**].allowed-origins=http://localhost:3000,http://localhost:4200
spring.cloud.gateway.globalcors.cors-configurations.[/**].allowed-methods=GET,POST,PUT,DELETE,OPTIONS
spring.cloud.gateway.globalcors.cors-configurations.[/**].allowed-headers=*
spring.cloud.gateway.globalcors.cors-configurations.[/**].allow-credentials=true
```

---

## 🔐 **Configuración de Seguridad**

```properties
security.gateway.secret=${GATEWAY_SECRET:myGatewaySecret123}
authorization.jwt.secret=${JWT_SECRET:AbCdEfGhIjKlMnOpQrStUvWxYz1234567890}
```

---

## ⏱️ **Configuración de Timeouts**

```properties
spring.cloud.gateway.httpclient.connect-timeout=3000
spring.cloud.gateway.httpclient.response-timeout=5s
```

---

## 📊 **Resumen de Arquitectura**

```
Cliente Frontend → API Gateway (8080) → Microservicio Específico
                                     ↓
                              Eureka Discovery (8761)
                                     ↓
                               Load Balancing
```

**Base URL para todas las peticiones:** `http://localhost:8080`