import express from "express";
import cors from "cors";
import { randomUUID } from "crypto";

const app = express();
app.use(express.json());
app.use(cors());

const store = {};

app.post("/store-cart", (req, res) => {
    const id = randomUUID();
    store[id] = req.body.cart;
    res.json({ id });
});

app.get("/get-cart", (req, res) => {
    const id = req.query.id;
    res.json({ cart: store[id] || null });
});

app.listen(process.env.PORT || 3000, () =>
    console.log("API running on port", process.env.PORT || 3000)
);
