### Register your webhook url

    POST /webhooks/register

###

    Request {
        url: string; // request
        token: string; // token to authenticate requests further
    }

###

    Brand {
        id: number;
        name: string;
    }

    Organization {
        id: number;
        user_id: number;
        type_id: number;
        name: string;
        logo: string;
        gst: string;
        incorporation_number: string;
        address: string;
        introduction: string;
        created_at: string;
        updated_at: string;
        city: string;
        state: string;
        pincode: string;
        country: string;
        domain?: any;
    }

    Category {
        id: number;
        name: string;
        description: string;
        meta_title: string;
        meta_des: string;
        meta_keywords: string;
        slug: string;
        parent_id?: any;
        status: number;
        sort: number;
    }

    Image {
        original: string;
    }

    Child {
        id: number;
        parent_id: number;
        value: string;
        quantity: number;
        price: string;
        sku?: any;
        is_variation: number;
        description?: any;
        specification?: any;
        weight?: any;
        length?: any;
        width?: any;
        height?: any;
        packagingLength?: any;
        packagingWidth?: any;
        packagingHeight?: any;
        title?: any;
        packagingWeight?: any;
        actual_amount: string;
        hsn_code?: any;
        gst?: any;
        attr_id: number;
        name: string;
        image: Image;
    }

    Attribute {
        id: number;
        parent_id: number;
        value: string;
        quantity: number;
        price: string;
        sku?: any;
        is_variation: number;
        description?: any;
        specification?: any;
        weight?: any;
        length?: any;
        width?: any;
        height?: any;
        packagingLength?: any;
        packagingWidth?: any;
        packagingHeight?: any;
        title?: any;
        packagingWeight?: any;
        actual_amount: string;
        hsn_code?: any;
        gst?: any;
        name: string;
        attr_id: number;
        children: Child[];
        image?: any;
    }

    Medium {
        id: number;
        mime: string;
        thumb: string;
        small: string;
        medium: string;
        large: string;
        original?: any;
        caption?: any;
        default: number;
        check: string;
        is_converted: number;
    }

    Attribute2 {
        id: number;
        name: string;
        value: string;
    }

    Image2 {
        large: string;
        medium: string;
    }

    Variation {
        id: number;
        name: string;
        sku: string;
        brand_name: string;
        amount: number;
        attributes: Attribute2[];
        image: Image2;
    }


    Product {
        id: number;
        name: string;
        slug: string;
        bdpin: string;
        brand_id: number;
        model: string;
        sku: string;
        description: string;
        specification: string;
        weight: string;
        length: string;
        width: string;
        height: string;
        amount: number;
        quantity: number;
        created_at: string;
        updated_at: string;
        min_price: string;
        max_price: string;
        shipping_charge: number;
        hsn_code: string;
        gst: string;
        packagingWeight: string;
        packagingLength: string;
        packagingWidth: string;
        packagingHeight: string;
        actual_amount: string;
        keywords?: any;
        parent_id?: any;
        has_shipping: number;
        redeemable?: any;
        brand_name: string;
        brand: Brand;
        organization: Organization;
        categories: Category[];
        attributes: Attribute[];
        rating?: any;
        media: Medium[];
        user_product?: any;
        variations: Variation[];
        isWishlist: number;
        wishlistCount: number;
    }

#### Each will be post request

### Creating

    Request {
        type: "product",
        token: string;
        action: "create",
        data: Product
    }

### Updating

    Request {
        type: "product";
        token: string;
        action: "create";
        data: Product; // only those which is update with id
    }

### Deleting

    Request {
        type: "product";
        token: string;
        action: "create";
        data: Product;
    }
