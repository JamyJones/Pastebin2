Using vanilla JavaScript to build a social media application that has potential to scale is not inherently stupid; however, **it is generally not advisable for large-scale or production-level applications**. Here’s why and what considerations to keep in mind:

---

### When Vanilla JavaScript Is Suitable
- **Prototyping & MVPs**: For rapid prototyping or minimum viable products where quick iteration is essential, vanilla JS can be effective.
- **Learning & Small Projects**: For educational purposes or very small projects with limited users and features, vanilla JS can suffice.
- **Simple Static Pages**: When only static or minimally interactive content is needed without complex state management.

---

### Challenges for Large-Scale, Feature-Rich Social Media Apps
1. **Complex State Management**
   - Social media apps involve complex UI states, real-time updates, notifications, etc.
   - Vanilla JS can handle simple interactions but becomes cumbersome as complexity grows.
   - **Solution**: Use front-end frameworks/libraries like React, Vue, or Angular for structured state management.

2. **Code Maintainability & Scalability**
   - As the codebase grows, vanilla JS code can become hard to maintain, test, and scale.
   - Modularization, component architecture, and build tools are standard to keep the code organized.
   - **Solution**: Use modern JS tooling and frameworks that encourage best practices.

3. **Performance Optimization**
   - Frameworks offer optimized rendering cycles.
   - Vanilla JS might require custom solutions for performance tweaks.

4. **Ecosystem & Tooling**
   - Frameworks provide integrations (CLI, testing, linting, routing, etc.) that streamline development.
   - With vanilla JS, you might need to manually integrate various tools.

5. **Development Speed & Collaboration**
   - Using established frameworks improves developer onboarding and collaboration.
   
---

### Best Practice Recommendations
- **For Front-End**:
  - Use a modern framework/library if expecting significant growth.
  - For smaller or simpler apps, vanilla JS with modular code can work but plan for future migration.
- **For Back-End**:
  - Use established frameworks (Express.js, Django, etc.) with REST/GraphQL APIs.
- **For Scalability**:
  - Design API and data storage with scalability in mind (e.g., microservices, cloud infrastructure).
  - Choose technologies that support horizontal scaling.

---

### Summary
**Vanilla JavaScript alone isn't "stupid," but it’s not a best practice for large, scalable social media applications.** The industry standard tends to favor frameworks that provide structure, scalability, maintainability, and a rich ecosystem, especially as the project grows in complexity.

---

### Example
**Simple React component vs vanilla JS**

*React (recommended for scalable front-end)*:
```jsx
import React, { useState, useEffect } from 'react';

function PostFeed() {
  const [posts, setPosts] = useState([]);

  useEffect(() => {
    fetch('/api/posts')
      .then(res => res.json())
      .then(data => setPosts(data));
  }, []);

  return (
    <div>
      {posts.map(post => (
        <div key={post.id}>{post.content}</div>
      ))}
    </div>
  );
}
export default PostFeed;
```

*Vanilla JS (for small, simple apps)*:
```html
<div id="posts"></div>
<script>
fetch('/api/posts')
  .then(res => res.json())
  .then(posts => {
    const container = document.getElementById('posts');
    posts.forEach(post => {
      const div = document.createElement('div');
      div.textContent = post.content;
      container.appendChild(div);
    });
  });
</script>
```

For larger projects, **the React approach is more maintainable and scalable**.

---

### Final Takeaway
While vanilla JS is a powerful tool, **building a highly scalable social media app typically requires leveraging modern frameworks, well-structured architecture, and scalable back-end solutions** to meet performance, maintainability, and development velocity standards expected in the industry.