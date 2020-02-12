# BIGLY API Documentation

### Note
    All response code has some meanings
    401 - Not login
    403 - Not allowed that specific data
    422 - validation error


    to make authentication request you need to provide token, you will receive by login api

## Authentication request

    header
    {
        Authorization: Bearer <token> // without bracket
    }

## API Endpoint
    https://app.bigly.io/api/v2

## Version Check

    GET /version

#### Response
    {
        "version": 2,
        "force": true,
        "message": "We did some major upgrades..."
    }

## Login

    POST /login

#### Request
    {
        "email": "some@email",
        "password": "some$password"
    }

#### Response
    {
        "token": "authentication token ...",
        "user": { /* User model */ }
    }

## Login / Register Truecaller

    POST /login/truecaller

#### Reqeust
    {
        "payload": "payload from sdk response",
        "signature": "signature from sdk",
        "device_token": "fcm token for notification",
        "referral_code": "ATMAX5"
    }

#### Response
    {
        // same as phone login
    }


##  Register through facebook (POST)

    POST /login/facebook

#### Request


    {
        "access_token" : "EAAF6lw...",
        "device_token" : "f5L9LXL2aOg:APA91b...",
        "device_type" : "ANDROID"
    }


#### Response


    {
        "token": "...",
        "user": {
            "id": 989,
            "name": "Gunjan Kumar",
            "username": null,
            "email": "1618242761564460@facebook.com",
            "phone": "9039541384",
            "data": {
                "facebook.id": "1618242761564460"
            }
        },
        "mobile": 1
    }

## Login by phone

    POST /login/phone

#### Request

    {
        "phone": "981818..."
        "referral_code": "ABC0123" // optional
    }

#### Response

    {
        "message" : "An otp has been sent to your phone"
    }


## Referrals 

### Tips

    GET /referral/tips

#### Response

    {
        "data": [
            "Online reselling is a new segement"
        ]
    }

### Banner

    GET /referral/banners

#### Response

    {
        "data": [
            {
                "id": 1,
                "path": "https://via.placeholder.com/350x150"
            }
        ]
    }


### Referral Amount Earned

    GET /referral/refers

#### Response
    {
        "current_page": 1,
        "data": [
            {
                "id": 2,
                "user_id": 32,
                "created_at": "2019-01-04 03:20:01",
                "amount": 2232,
                "user": {
                    "id": 32,
                    "name": "Being Adam"
                }
            }
        ],
        "from": 1,
        "last_page": 1,
        "next_page_url": null,
        "path": "http://localhost:8000/api/v2/referral/refers",
        "per_page": 15,
        "prev_page_url": null,
        "to": 1,
        "total": 1
    }

### Referral Paymnets

    GET /referral/redeems

#### Response

    {
    "current_page": 1,
        "data": [
            {
                "id": 566,
                "amount": "100.00",
                "created_at": "2019-01-15 00:27:16",
                "order_id": 1064,
                "item": "Always Fit Anti Radiation Mobile Chip"
            }
        ],
        "from": 1,
        "last_page": 1,
        "next_page_url": null,
        "path": "http://localhost:8000/api/v2/referral/payments",
        "per_page": 15,
        "prev_page_url": null,
        "to": 1,
        "total": 1
    }


### Referral Terms and condition

Webview

    GET https://app.bigly.io/referral/terms

### Response

    HTML Response ( to be used as webview )


## Tutorials

### Show all tutorials

    GET /tutorials

#### Request
    {
        "data": [
            {
                "title": "How to Start Your Reselling Business Online with Bigly",
                "thumb": "",
                "media": "https://www.youtube.com/watch?v=OaBtVF3u8HY",
                "duration": 130
            }
        ],
        "current_page": 1,
        "total": 1
    }

## Verify Otp to complete login

    POST /login/phone/verify

#### Request

    {
        "phone": "9818...",
        "otp" : 4359,
        "referral_code": "ABC0123" // same as login
    }

#### Response

    {
        "token": "...",
        "user": {
            "id": 989,
            "name": "Gunjan Kumar",
            "username": null,
            "email": "1618242761564460@facebook.com",
            "phone": "9039541384",
        }
    }


## Signup as supplier
    POST /register/supplier

#### Request
    {
        "name": "...",
        "email": "...@...",
        "phone": "...",
        "password": "..."
    }

#### Response
    {
        "status": "ok",
        "message": "Success message",
        "data": {
            "id": 989,
            "name": "Name",
            "username": null,
            "email": "abc@abc.com",
            "phone": "123456"
        }
    }


## Profile

    GET /profile

#### Response

    {
        "id": 6340,
        "name": "adil",
        "username": null,
        "email": "md-dil@live.com",
        "status": 1,
        "phone": null,
        "address": {
            "id": 16,
            "name": "adil",
            "email": "md-dil@live.com",
            "phone": "9818128797",
            "address": "",
            "street": "",
            "pincode": "110050",
            "landmark": null,
            "city": "New Delhi",
            "state": "Delhi",
            "area": null,
            "colony": null,
            "country": null
        },
        "referral_code": "3KWWKC",
        "wallet": {
            "id": 5,
            "user_id": 6340,
            "credit": 0,
            "created_at": "2018-12-26 03:58:07",
            "updated_at": "2018-12-26 03:58:07"
        }
    }

## Update Profile

    PUT /profile

#### Request
    {
        "name": "Name",
        "email": "someone@emai.com"
    }

#### Response
    {
        message: ok
    }

### Wallet or Credit
    GET /profile/wallet

#### Response
    {
        "credit": 12343,
        "redeemable": 12,
        "rate": "fixed" or "percent"
    }

### Wallet referral code apply

    POST /profile/referral/apply

#### Request
    {
        "referral_code": "ABC110"
    }

#### Response

    {
        "status": "ok",
        "message": "Referral Code has ..you w...as been credit with Rs. 500"
    }


## Get all the products in pagination . Per page 15 products

    GET /products?q=query&category[]=51&vendor[]=514&vendor[]=2&price_range=501-1000


#### Response

    {
        "from": 1,
        "last_page": 67,
        "next_page_url": "/products?page=2",
        "path": "/products",
        "per_page": 15,
        "prev_page_url": null,
        "to": 15,
        "total": 1003
        "current_page": 1,
        "data": [
            {
                "id": 1011,
                "name": "sZEfgfr",
                "amount": 1234,
                "brand_name": "dsgesdge",
                "redeemable": 30,
                "media": {
                    "thumb": "http://s.bigly.io/products/thumb/zkqr1y4lujen9ks-9htf1uw.jpg",
                    "large": "http://s.bigly.io/products/large/zkqr1y4lujen9ks-9htf1uw.jpg",
                }
            },
            ...
        ]
           
    }


## Top selling products

    GET - /products/top-selling?q=query&category[]=51&vendor[]=514&vendor[]=2&price_range=501-1000

#### Response

    {
        "from": 1,
        "last_page": 67,
        "next_page_url": "/products?page=2",
        "path": "/products",
        "per_page": 15,
        "prev_page_url": null,
        "to": 15,
        "total": 1003
        "current_page": 1,
        "data": [
            {
                "id": 1011,
                "name": "sZEfgfr",
                "amount": "21.00",
                "quantity": 533,
                "isWishlist": true,
                "brand_name": "dsgesdge",
                "redeemable": 30,
                "media": {
                    "thumb": "http://s.bigly.io/products/thumb/zkqr1y4lujen9ks-9htf1uw.jpg",
                    "large": "http://s.bigly.io/products/large/zkqr1y4lujen9ks-9htf1uw.jpg",
                }
            }
        ...
    ],



## Get Specific Product 

    GET /products/29620


#### Response

    {
        "id": 29620,
        "name": "TrendzWinG Grey Fuck Rules T-shirt",
        "slug": "trendzwing-grey-fuck-rules-t-shirt-tw151",
        "bdpin": "73B4",
        "brand_id": 256,
        "model": "TW151",
        "sku": "TW151",
        "description": "We bring you the designs that tickle your like and enhance your personality leaving a trend anywhere you go!. It is bio washed to ensure one can get the soft and fluffy feeling of the tee.",
        "specification": "Colour: Grey\nFabric: 100 % Cotton 180GSM with bio-washed\nOccasion: Casual\nGender: Men\nSleeve Type: Short Sleeve",
        "weight": "200.00",
        "length": "30.00",
        "width": "25.00",
        "height": "5.00",
        "amount": 331,
        "quantity": 20,
        "created_at": "2018-09-13 15:43:52",
        "updated_at": "2018-09-13 16:24:23",
        "min_price": "261.00",
        "max_price": "499.00",
        "shipping_charge": 0,
        "hsn_code": "",
        "gst": "5.00",
        "packagingWeight": "200.00",
        "packagingLength": "23.00",
        "packagingWidth": "25.00",
        "packagingHeight": "5.00",
        "actual_amount": "0.00",
        "keywords": null,
        "parent_id": null,
        "has_shipping": 0,
        "redeemable": null,
        "brand_name": "TrendzWinG",
        "brand": {
            "id": 256,
            "name": "TrendzWinG"
        },
        "organization": {
            "id": 1271,
            "user_id": 1270,
            "type_id": 10,
            "name": "Trendzwing Collection",
            "logo": "",
            "gst": "27AQTPJ3704F1ZR",
            "incorporation_number": "",
            "address": "Shop No. 5/5, Ground Floor, Mahavir Jyot Chs Ltd, Station Road, Bhayander (West)",
            "introduction": "Shop for the trendiest collection of T shirts for men. With a variety of cool and classy colours and designs that we have explore for you. We make a hot match of fabric, trend, colour and pattern to suit you and make your personality elegant.",
            "created_at": "2018-06-16 13:43:39",
            "updated_at": "2018-06-17 13:29:16",
            "city": "Thane",
            "state": "Maharashtra",
            "pincode": "401101",
            "country": "India",
            "domain": null
        },
        "categories": [
            {
                "id": 55,
                "name": "Men's Clothing",
                "description": "",
                "meta_title": "",
                "meta_des": "",
                "meta_keywords": "",
                "slug": "",
                "parent_id": null,
                "status": 1,
                "sort": 100
            }
        ],
        "attributes": [
            {
                "id": 10918,
                "parent_id": 0,
                "value": "Grey",
                "quantity": 20,
                "price": "261.00",
                "sku": null,
                "is_variation": 1,
                "description": null,
                "specification": null,
                "weight": null,
                "length": null,
                "width": null,
                "height": null,
                "packagingLength": null,
                "packagingWidth": null,
                "packagingHeight": null,
                "title": null,
                "packagingWeight": null,
                "actual_amount": "0.00",
                "hsn_code": null,
                "gst": null,
                "name": "Color",
                "attr_id": 1,
                "children": [
                    {
                        "id": 10919,
                        "parent_id": 10918,
                        "value": "S",
                        "quantity": 5,
                        "price": "261.00",
                        "sku": null,
                        "is_variation": 1,
                        "description": null,
                        "specification": null,
                        "weight": null,
                        "length": null,
                        "width": null,
                        "height": null,
                        "packagingLength": null,
                        "packagingWidth": null,
                        "packagingHeight": null,
                        "title": null,
                        "packagingWeight": null,
                        "actual_amount": "0.00",
                        "hsn_code": null,
                        "gst": null,
                        "attr_id": 2,
                        "name": "Size",
                        "image": null
                    },
                    {
                        "id": 10920,
                        "parent_id": 10918,
                        "value": "M",
                        "quantity": 5,
                        "price": "261.00",
                        "sku": null,
                        "is_variation": 1,
                        "description": null,
                        "specification": null,
                        "weight": null,
                        "length": null,
                        "width": null,
                        "height": null,
                        "packagingLength": null,
                        "packagingWidth": null,
                        "packagingHeight": null,
                        "title": null,
                        "packagingWeight": null,
                        "actual_amount": "0.00",
                        "hsn_code": null,
                        "gst": null,
                        "attr_id": 2,
                        "name": "Size",
                        "image": null
                    },
                    {
                        "id": 10921,
                        "parent_id": 10918,
                        "value": "L",
                        "quantity": 5,
                        "price": "261.00",
                        "sku": null,
                        "is_variation": 1,
                        "description": null,
                        "specification": null,
                        "weight": null,
                        "length": null,
                        "width": null,
                        "height": null,
                        "packagingLength": null,
                        "packagingWidth": null,
                        "packagingHeight": null,
                        "title": null,
                        "packagingWeight": null,
                        "actual_amount": "0.00",
                        "hsn_code": null,
                        "gst": null,
                        "attr_id": 2,
                        "name": "Size",
                        "image": null
                    },
                    {
                        "id": 10922,
                        "parent_id": 10918,
                        "value": "XL",
                        "quantity": 5,
                        "price": "261.00",
                        "sku": null,
                        "is_variation": 1,
                        "description": null,
                        "specification": null,
                        "weight": null,
                        "length": null,
                        "width": null,
                        "height": null,
                        "packagingLength": null,
                        "packagingWidth": null,
                        "packagingHeight": null,
                        "title": null,
                        "packagingWeight": null,
                        "actual_amount": "0.00",
                        "hsn_code": null,
                        "gst": null,
                        "attr_id": 2,
                        "name": "Size",
                        "image": {
                            "original": "https://s.bigly.io/products/attributes/original/rzlan7o9klwgiok-3c8234d139.jpg"
                        }
                    }
                ],
                "image": null
            }
        ],
        
        "rating": null,
        "media": [
            {
                "id": 93662,
                "mime": "image/jpeg",
                "thumb": "https://s.bigly.io/products/thumb/uhyyq6bjxeg1tj6-a-cnmtrw.jpeg",
                "small": "https://s.bigly.io/products/small/uhyyq6bjxeg1tj6-a-cnmtrw.jpeg",
                "medium": "https://s.bigly.io/products/medium/uhyyq6bjxeg1tj6-a-cnmtrw.jpeg",
                "large": "https://s.bigly.io/products/large/uhyyq6bjxeg1tj6-a-cnmtrw.jpeg",
                "original": null,
                "caption": null,
                "default": 1,
                "check": "pending",
                "is_converted": 1
            },
            {
                "id": 93663,
                "mime": "image/jpeg",
                "thumb": "https://s.bigly.io/products/thumb/inerdtwmppv53fc-j19wchca.jpeg",
                "small": "https://s.bigly.io/products/small/inerdtwmppv53fc-j19wchca.jpeg",
                "medium": "https://s.bigly.io/products/medium/inerdtwmppv53fc-j19wchca.jpeg",
                "large": "https://s.bigly.io/products/large/inerdtwmppv53fc-j19wchca.jpeg",
                "original": null,
                "caption": null,
                "default": 0,
                "check": "pending",
                "is_converted": 1
            }
        ],
        "user_product": null,
        "variations": [
        {
            "id": 29708,
            "name": "Dashk Long Crush Curtains Digital",
            "sku": "DSK-SND264",
            "brand_name": "Dashk",
            "amount": 100,
            "attributes": [
                {
                    "id": 1,
                    "name": "Color",
                    "value": "Red"
                },
                {
                    "id": 2,
                    "name": "Size",
                    "value": "9*4"
                }
            ],
            "image": {
                "large": "https://s.bigly.io/products/large/wt5tdeqyjxut7qi-screenshot.png",
                "medium": "https://s.bigly.io/products/medium/wt5tdeqyjxut7qi-screenshot.png"
            }
        },
        {
            "id": 29709,
            "name": "Dashk Long Crush Curtains Digital Print New Trendy Design Size (7*4 Feet) Multy Color",
            "sku": "DSK-SND265",
            "brand_name": "Dashk",
            "amount": 200,
            "attributes": [
                {
                    "id": 2,
                    "name": "Size",
                    "value": "7*4"
                },
                {
                    "id": 1,
                    "name": "Color",
                    "value": "Blue"
                }
            ],
            "image": {
                "large": "https://s.bigly.io/products/large/s8n4g110xxx8p0v-screenshot.png",
                "medium": "https://s.bigly.io/products/medium/s8n4g110xxx8p0v-screenshot.png"
            }
        },
        "isWishlist": 0,
        "wishlistCount": 0
    }



## To Delete the product (DELETE)

    DELETE /products/11


#### Response

    {
        "message": "Product has been deleted successfully"
    }

## Update Product

    PUT /products/1007

#### Request

    {
        "name": "cfdsgvd",
        "amount" : 54,
        "categories": [
            {
                "id": 1,
                "name": "Clothes"
            }
        ]
    }


## Shared products

    GET /products/shared

#### Response 

    // same as /products api 



## Shared products

    PUT /products/shared

#### Request 

    {
        "product_id": 1234,
        "platform": "facebook" // or "whatsapp"
    }

#### Response

    {
        "id": 73482,
        "user_id": 6340,
        "product_id": 11821,
    }

## Get wishlists

    GET /wishlists

#### Response

    same as product response

### Add wishlist

    POST /wishlists

### _Request_

    {
        "product": 1
    }

## Carts

    GET /carts

#### Response

    {
        "current_page": 1,
        "data": [
            {
                "id": 6615,
                "quantity": 1,
                "product_id": 27381,
                "attribute_id": 4833,
                "product": {
                    "id": 27381,
                    "name": "Nikhaar Designers Khadi Kurti With Embroidery And Seperate Long Inner",
                    "amount": "1199.00",
                    "brand_name": "",
                    "brand": null,
                    "redeemable": 30,
                    "default_media": {
                        "thumb": "https://s.bigly.io/products/thumb/zwrwoaydy9xeanb-dl-01.jpg",
                        "large": "https://s.bigly.io/products/large/zwrwoaydy9xeanb-dl-01.jpg"
                    }
                },
                "attribute": {
                    "id": 4833,
                    "value": "34",
                    "attr_id": 2,
                    "name": "Size"
                }
            }
            ...
        ],
        "from": 1,
        "last_page": 1,
        "next_page_url": null,
        "path": "http://localhost:8000/api/v2/carts",
        "per_page": 15,
        "prev_page_url": null,
        "to": 5,
        "total": 5
    }


## Verify shipment against cart.

    GET /carts/{cart}/verify-shipment/{address}

#### Response
    {
        "status": "ok",
        "shipment": true
    }


    PUT /profile/bank
    GET /profile/bank

    GET /profile/validate/address

#### Response
    {
        "status": "ok",
        "valid": (boolean) true
    }

### API raw details


    resource /addresses

    // Wishlists and carts

    POST /wishlists/{wishlist}/add-to-cart

    POST /wishlists/products/{product}/add-to-cart

    RESOURCE /wishlists

    RESOURCE /carts

    POST /carts/{cart}/create-order

#### Request
    {
        response_id: <payment id>,
        quantity: <quantity to buy>,
        amount: <edited amount by seller>,
        address_id: <selected address id>,
        is_redeem: <boolean>
    }

### Orders


    RESOURCE /orders
    GET /orders/user/{id}
    POST /orders/{order}/cancel

## Orders

    GET /orders

#### Response

    {
        "current_page": 1,
        "data": [
            {
                "id": 1044,
                "user_id": 6340,
                "client_id": 0,
                "name": "APP_Order_NvgM9fy1ZgbDREoe",
                "invoice": "",
                "amount": "299.00",
                "created_at": "2018-11-04 20:51:54",
                "updated_at": "2018-11-04 20:51:54",
                "status": "completed",
                "price": "2990.00",
                "payment_method": "PREPAID",
                "returnable": true,
                "cancelable": true,
                "item": {
                    "name": "TT Bags Bkpk-21 15 L Backpack (Orange)",
                    "quantity": 10,
                    "photo": {
                        "thumb": "1513598471-bkpk-21-bag8-backpack-tt-bags-original-imaevmkggcumfmgh.jpeg"
                    }
                }
            }
        ],
        "from": 1,
        "last_page": 1,
        "next_page_url": null,
        "path": "http://localhost:8000/api/v2/orders",
        "per_page": 15,
        "prev_page_url": null,
        "to": 2,
        "total": 2
    }

### Find order Detail

    GET /orders/<id>

#### Response
    {
        "id": 1083,
        "user_id": 6351,
        "client_id": 0,
        "name": "APP_Order_ot6gj3LEi9rjq76f",
        "invoice": "",
        "amount": "470.00",
        "created_at": "2019-01-26 00:32:59",
        "updated_at": "2019-01-26 00:32:59",
        "status": "completed",
        "price": "900.00",
        "payment_method": "cod",
        "type": null,
        "parent_id": null,
        "redeemed_amount": "30.00", // optional key
        "items": [
            {
                "id": 1025,
                "order_id": 1083,
                "product_id": 911,
                "attribute_id": 0,
                "name": "Right Choice Super Multi Stylish Tuff Quality (Black Pink)",
                "quantity": 1,
                "amount": 825,
                "organization_id": 13,
                "status": "completed",
                "shipment_id": "6143461083",
                "shipping_charge": "75.00",
                "transfer_price": "395.00",
                "attribute_transfer_price": "0.00",
                "packaging_weight": "0.00",
                "packaging_length": "0.00",
                "packaging_width": "0.00",
                "packaging_height": "0.00",
                "product": {
                    "id": 911,
                    "name": "Right Choice Super Multi Stylish Tuff Quality (Black Pink)",
                    "slug": "401/right-choice-super-multi-stylish-tuff-quality-black-pink",
                    "brand": {
                        "id": 12,
                        "name": "Right Choice Bags"
                    },
                    "default_media": {
                        "thumb": "http://localhost:8000/media/thumb/1514609339-71nfwnzd2ql-ul1500.jpg",
                        "large": "http://localhost:8000/media/large/1514609339-71nfwnzd2ql-ul1500.jpg",
                    }
                },
                "attribute": null
            }
        ],
        "addresses": [
            {
                "id": 1633,
                "order_id": 1083,
                "name": "MD Adil",
                "email": "",
                "mobile": "9818128797",
                "address_line_1": "dfasfdaf",
                "address_line_2": "Something",
                "pincode": "110055",
                "city": "New Delhi",
                "state": "Delhi",
                "country": "India",
                "type": "billing"
            }
        ]
    }


## Products

    GET /products/{product}/shipment/availability?pincode=112233
    

#### Response
    {
        "status": "ok",
        "shipment": false,
        "prepaid": false,
        "cod": false,
        "message": "Shipment service is not available"
    }

### Get Vendors

    GET /products/vendors

    GET /products/categories

#### Request

    &parent=1

#### Response
    {
        "current_page": 1,
        "data": [
            {
                "id": 157,
                "name": "Jewellery",
                "media": {
                    "thumb": "https://s.bigly.io/categories/1528449908-MZGH1mmL9ppaYux.jpeg"
                }
            }
        ],
        "from": 1,
        "last_page": 1,
        "next_page_url": null,
        "path": "http://localhost:8000/api/v2/products/categories",
        "per_page": 200,
        "prev_page_url": null,
        "to": 1,
        "total": 1
    }


    // Products

    GET /products/latest
    GET /products/top-selling
    resource /products

    // Queries
    resource /queries.comments

## Reply on query

    POST /queries/{query}/comments
#
### Request

    {
        "message": "Commect message"
    }

#### Response
    
    {
        // comment object
    }

    resource /queries


## Cancel Reasons
    GET /orders/cancel-reasons

#### Response
    {
        "data": [
            {
                "id": 18,
                "reason": "Order Created by Mistake"
            }
        ]
    }


## Return Reasons
    GET /orders/return-reasons

#### Response
    {
        "data": [
            {
                "id": 18,
                "reason": "Order Created by Mistake"
            }
        ]
    }


## Track Order
    GET /orders/<id>/track

#### Response
    {
        "status": "incomplete",
        "id": 1234,
        "awbNo": 21232,
        "childAwbID": null,
        "carrierName": "Carrier Name",
        "events": [
            {
                "status": "OD",
                "Remarks": "Out for delivery (Dispatched)",
                "Location": "AMD_Satellite (Gujarat)",
                "Time": "2018-10-22T09:33:13.840Z"
            }
        ]
    }


    PUT /orders/{order}/request-return

##### Request
    {
        "comment": "Why you want to return this product"
    }

##### Response
    {
        "status": "ok",
        "message": "Return request has been post successfully"
    }

## Order Status

    GET /orders/user/{id}/status/{status}

## Notifications

    GET /notifications
    GET /settings/notification
    POST /settings/notification

    // Static pages

    GET /faqs

    GET /terms-condition

## REsponse
    HTML page

    // Tokens
    GET /tokens/fcm

    PUT /tokens/fcm

## Rewards

### Show all rewards

    GET /rewards

#### Response
    {
        "data": [
            {
                "id": 1,
                "title": "This is .Reward",
                "image": "http://localhost:8000/absc"
            }
        ]
    }


### Find reward description

    GET /rewards/{reward}

#### Response
    {
        "id": 1,
        "title": "This is .Reward",
        "description": "fasdfa",
        "image": "http://localhost:8000/absc"
    }

## Ad Banners

    GET /ads/banners

#### Response

    {
        "data": [
            {
                "link": "thisistheproductlink",
                "image": "http://localhost:8000/media/large/1513847769-41wqjktzzjl.jpg"
            }
        ]
    }

## Payments Reporting

### Reports Home

    GET /reports/payments/home

#### Response

    {
        "nextPaymentDate": "2019-01-15 14:46:46",
        "lastReceived": null,
        "totalReceived": 0,
        "totalOrders": "5000.00",
        "pending": 5000,
        "hasBank": false,
        "notes": [
            "We transfer payments on 5th of each month"
        ]
    }

### All Payments

    GET /reports/payments

#### Response
    {
        "current_page": 1,
        "data": [
            {
                "id": 1,
                "channel": " ",
                "amount": "1000.00",
                "created_at": "2019-01-04 19:41:01"
            }
        ],
        "from": 1,
        "last_page": 1,
        "next_page_url": null,
        "path": "http://localhost:8000/api/v2/reports/payments",
        "per_page": 15,
        "prev_page_url": null,
        "to": 1,
        "total": 1
    }


### Payment Detail

    GET /reports/payments/<id>

#### Response
    {
        "id": 1,
        "user_id": 6340,
        "order_ids": " ",
        "channel": " ",
        "amount": "1000.00",
        "res_id": " ",
        "status": 1,
        "created_at": "2019-01-04 19:41:01",
        "updated_at": "2019-01-04 19:41:09",
        "orders": [
            {
                "id": 41,
                "user_id": 336,
                "client_id": 336,
                "name": "DS_Order_6oLU0tPqhnzCpRg7",
                "invoice": "",
                "amount": "99.00",
                "created_at": "2018-03-10 09:45:17",
                "updated_at": "2018-03-10 09:45:28",
                "status": "",
                "price": "99.00",
                "payment_method": "cod",
                "type": null,
                "parent_id": null,
                "pivot": {
                    "user_order_payment_id": 1,
                    "order_id": 41
                }
            }
        ]
    }

## logout

    POST /logout

### Unregister

    POST /logout/unregister

#### Response
    {
        "status": "ok",
        "message": "User has been deleted" 
    }

