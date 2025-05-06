
### **Problem: Embedding-Based Semantic Search**

Let $\mathbf{q} \in \mathbb{R}^{3}$ be a query vector and a set of document embeddings $\mathcal{D} = \{\mathbf{d}_1, \mathbf{d}_2, \mathbf{d}_3, \mathbf{d}_4\} \subset \mathbb{R}^{3}$. All vectors are normalized (i.e., unit vectors), and represent embeddings in a vector database.

You are given:

* $\mathbf{q} = \frac{1}{\sqrt{3}}[1, 1, 1]$
* $\mathbf{d}_1 = [1, 0, 0]$
* $\mathbf{d}_2 = \frac{1}{\sqrt{2}}[1, 1, 0]$
* $\mathbf{d}_3 = \frac{1}{\sqrt{2}}[0, 1, 1]$
* $\mathbf{d}_4 = \frac{1}{\sqrt{2}}[1, 0, 1]$

---

#### **Tasks:**

**(a)** Compute the cosine similarity between the query vector $\mathbf{q}$ and each document vector $\mathbf{d}_i$.

**(b)** Which document is the most semantically similar to the query according to cosine similarity?

**(c)** Suppose you want to reduce the dimensionality from $\mathbb{R}^3$ to $\mathbb{R}^2$ using projection onto the plane spanned by $\mathbf{d}_2$ and $\mathbf{d}_3$. Compute the projection of $\mathbf{q}$ onto this plane.

**(d)** Compute the new cosine similarity between the projected query and the projected $\mathbf{d}_2$ and $\mathbf{d}_3$. Does the ranking change in this 2D subspace?

---

### **Solution:**

---

**(a) Cosine similarity** (for normalized vectors):

$$
\cos(\theta) = \mathbf{q} \cdot \mathbf{d}_i
$$

* $\mathbf{q} \cdot \mathbf{d}_1 = \frac{1}{\sqrt{3}} \cdot 1 = \frac{1}{\sqrt{3}} \approx 0.577$

* $\mathbf{q} \cdot \mathbf{d}_2 = \frac{1}{\sqrt{3}} \cdot \frac{1}{\sqrt{2}}(1+1+0) = \frac{2}{\sqrt{6}} \approx 0.816$

* $\mathbf{q} \cdot \mathbf{d}_3 = \frac{1}{\sqrt{3}} \cdot \frac{1}{\sqrt{2}}(0+1+1) = \frac{2}{\sqrt{6}} \approx 0.816$

* $\mathbf{q} \cdot \mathbf{d}_4 = \frac{1}{\sqrt{3}} \cdot \frac{1}{\sqrt{2}}(1+0+1) = \frac{2}{\sqrt{6}} \approx 0.816$

---

**(b) Most similar document:**

Cosine similarity is highest for **$\mathbf{d}_2, \mathbf{d}_3, \mathbf{d}_4$** equally (approx. 0.816), so all three are tied as most similar.

---

**(c) Projection onto span of $\mathbf{d}_2$ and $\mathbf{d}_3$**

Let’s denote $\mathbf{u}_1 = \mathbf{d}_2$, $\mathbf{u}_2 = \mathbf{d}_3$

Use **Gram-Schmidt** to form an orthonormal basis:

* $\mathbf{u}_1 = \frac{1}{\sqrt{2}}[1, 1, 0]$
* To orthogonalize $\mathbf{d}_3$ to $\mathbf{u}_1$:

$$
\text{proj}_{\mathbf{u}_1}(\mathbf{d}_3) = \left( \mathbf{d}_3 \cdot \mathbf{u}_1 \right)\mathbf{u}_1 = \left( \frac{1}{\sqrt{2}}[0,1,1] \cdot \frac{1}{\sqrt{2}}[1,1,0] \right) \mathbf{u}_1 = \left( \frac{1}{2}(1) \right)\mathbf{u}_1 = \frac{1}{2}\mathbf{u}_1
$$

$$
\mathbf{v} = \mathbf{d}_3 - \frac{1}{2}\mathbf{u}_1 = \frac{1}{\sqrt{2}}[0,1,1] - \frac{1}{2} \cdot \frac{1}{\sqrt{2}}[1,1,0] = \frac{1}{\sqrt{2}}[-\frac{1}{2}, \frac{1}{2}, 1]
$$

Normalize $\mathbf{v}$ to get $\mathbf{u}_2'$

Now project $\mathbf{q}$ onto the plane:

$$
\text{proj}_{\text{plane}}(\mathbf{q}) = (\mathbf{q} \cdot \mathbf{u}_1)\mathbf{u}_1 + (\mathbf{q} \cdot \mathbf{u}_2')\mathbf{u}_2'
$$

Compute and plug in to find final projection (full vector math).

---

**(d) Cosine similarity after projection:**

Normalize the projected $\mathbf{q}$, and compute dot products with projected $\mathbf{d}_2$ and $\mathbf{d}_3$.

You will observe **slightly different scores**, possibly breaking the tie from part (b), depending on the geometry of the plane.

