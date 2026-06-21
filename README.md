# 🎓 University Graph Database — Neo4j

> A graph-based university database built with **Neo4j** and **Cypher Query Language**

---

## 🗂️ Graph Structure
---

## 🟣 Nodes

| Icon | Node | Description |
|------|------|-------------|
| 👨‍🎓 | `Student` | University students |
| 📚 | `Course` | Available courses |
| 👨‍🏫 | `Instructor` | Course instructors |
| 🏛️ | `Department` | Academic departments |

---

## 🔗 Relationships

| Relationship | From | To |
|---|---|---|
| `ENROLLED_IN` | Student | Course |
| `TEACHES` | Instructor | Course |
| `BELONGS_TO` | Student/Course | Department |

---

## 🔍 Queries

### 1️⃣ Find all students in a course
```cypher
MATCH (s:Student)-[:ENROLLED_IN]->(c:Course)
RETURN c.name AS Course, collect(s.name) AS Students
```

### 2️⃣ Find instructors teaching more than one course
```cypher
MATCH (i:Instructor)-[:TEACHES]->(c:Course)
WITH i, count(c) AS numCourses
WHERE numCourses > 1
RETURN i.name AS Instructor, numCourses AS NumberOfCourses
```

### 3️⃣ Find departments with the most students
```cypher
MATCH (s:Student)-[:BELONGS_TO]->(d:Department)
RETURN d.name AS Department, count(s) AS NumberOfStudents
ORDER BY NumberOfStudents DESC
```

### 4️⃣ Recommend courses based on similar enrollments
```cypher
MATCH (s:Student)-[:ENROLLED_IN]->(c:Course)<-[:ENROLLED_IN]-(other:Student)
MATCH (other)-[:ENROLLED_IN]->(rec:Course)
WHERE NOT (s)-[:ENROLLED_IN]->(rec)
RETURN s.name AS Student, collect(DISTINCT rec.name) AS RecommendedCourses
```

---

## 🛠️ Tools Used

![Neo4j](https://img.shields.io/badge/Neo4j-008CC1?style=for-the-badge&logo=neo4j&logoColor=white)
![Cypher](https://img.shields.io/badge/Cypher-Query-blueviolet?style=for-the-badge)

---

## 📸 Graph Preview

> See screenshots in the repository for full graph visualization!
