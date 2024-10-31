java c
CS770/870 Assignment 6
•  Due: Tuesday, October 29th, 2024
•  Late penalty: Wed -5%,Thu -100% <—– ONLY ONE DAY LATE ALLOWED!
Ray Casting
For this assignment, you will compute the geometric steps in a ray caster.  It will give you experience needed when implementing a ray tracer in upcoming assignments.
The Scene and Camera
Consider a scene with the following three objects:
•  there is a sphere with these parameters:
– center C = (1 0 1)
–  radius R = 2
•  there is a triangle with these vertices:
– A = (3 -1 -1)
–  B = (3 -1 +1)
– C = (1 3 0)
•  there is a cylinder, with these parameters:
–  axis aligned with theY axis
–  center at (2 0 0)
–  radius R = 1
–  height (top to bottom) = 4
There is a perspective camera, with the following parameters:
• eye = (6 1 0)
•  lookat = (0 1 0)
• vup = (0 1 0)
The image plane has these parameters:
•  (clipLe什, clipRight) = (-2, 2)
•  (clipBottom, clipTop) = (-1, 1)
• clipNear = 2
The image plane is divided into
•  W = 401 pixels across
•  H = 301 pixels up-down


Exercises
Consider a pixel with PDCS  = (xDCS yDCS ) = (200 150). Perform. the following calculations. Then find the object which
the ray (which starts at the pixel) hits first.
1.  Get the ray’s starting pointS and direction vector V:
a)  Transform. the pixel PDCS from DCS (device coordinates, also called pixel coordinates) to VCS (view coordinates, also called camera coordinates). Obtain PVCS, and print it.
b)  Obtain the three basis vectors of the VCS system, Xvcs, Yvcs, and Zvcs, and print them, on separate lines.
c)  Compute MV CS→WCS , the inverse of the view matrix, and print it.
d)  Use this matrix to obtain PW CS, the pixel’s world coordinates, and print it.
e)  Obtain a unit-length vector V in the direction from the eye to the pixel, and print it. You now have a ray P = S + tV, where S is PW CS . 
2.  Compute the point Ps where the ray hits the sphere. The sphere’s equation is (P — C) · (P — C) = R2
To do this, substitute the ray’s equation P = S + tV into the sphere’s equation. You should get a quadratic equation in t.
a)  solve for t
b)  check that tis positive
c)  if there are 2 positive roots, pick the smaller one
d)  plug back into Ps  = S + tV to get the hit point.
Then, Get the surface normal at the hit point: N = Ps  — C. Normalize this vector, and print it.
e)  For this question, print each of the following on a separate line:
•  the quadratic’s coeficients, a, b, c,
•  the discriminant d,
•  the ray parameter t,
•  the hit point, and
•  the surface normal.
3.  Now compute the point Pt where the ray hits the triangle, as follows.
a) A point Pt on the triangle will have barycentric coordinates (uv), and will obey this equation: Pt  = A + u(B —
A) + v(C — A). The barycentric coordinates must obey:
•  0 ≤ u ≤ 1


•  0 ≤ v ≤ 1
• u + v ≤ 1
b) The point Pt will also be on the ray: Pt  = S + tV
c) Join the equations: A + u(B — A) + v(C — A) = S + tV
d)  This is actually three equati代 写CS770/870 Assignment 6C/C++
代做程序编程语言ons (one for x, one for y, and one for z). Obtain a 3x3 linear system of equations for t, u, and v.
e)  Solve the equations. There is true hit if tis positive, and both u and v obey the barycentric conditions.
f)  Get the surface normal of the triangle: N = (B — A) × (C — A). Normalize this vector, and print it.
g)  For this question, print each of the following on a separate line:
•  The 3 × 3 matrix on the le什 side of the equation,
•  the right-hand side of the matrix equation,
• the valuesoft, u, and v,
•  the hit point, and
•  the surface normal.
4.  Compute the point Pc where the ray intersects the cylinder. Proceed as follows:
a)  Get the equation for the top cap of the cylinder. It is a plane, plus a constraint:
•  Point on plane Q = center + height/2 * (0 1 0)
•  Normal to plane N = (0 1 0)
•  Inside circle: (x — center.x)2  + (z — center.z)2  < radius2 .
Find the ray’s intersection with the plane. If it exists (plane isn’t parallel to the ray), check if the hit point is inside the circle.
b)  Repeat for the bottom cap:
•  Point on plane Q = center — height/2 * (0 1 0)
•  Normal to plane N = (0  — 1 0)
c)  Get the ray’s intersection with the cylinder’s tube. It is a bounded cylinder, which can be expressed as a circle, with a constraint:
•  (x — center.x)2 + (z — center.z)2  = radius2 ,
• center.y — height/2 ≤ y, and $ y ≤ center.y + height/2.
To intersect this with the ray, plug the ray equation:
• Pc = S + tV
into the circle equation:
•  (S.x + tV.x — center.x)2 + (S.z + tV.z — center.z)2  — radius2 = 0
Which gives you a quadratic equation in t: at2 + bt + c = 0, where
• a = V.x2 + V.z2
• b = 2(S.x — center.x)V.x + 2(S.z — center.z)V.z
• c = (S.x — center.x)2 + (S.z — center.z)2  — radius2
Solve, just like for a sphere,for the smallest positive value of t, and plug it into the ray equation to get Pc.
d)  Check if y is in bounds.
e)  If so, compute the surface normal:
• N = (Pc.x, 0, Pc.z), normalized.
f)  Gather all the hits you obtained in steps a), b),and d), and get the one with the smallest ray parameter t.
g)  Print, on separate lines,
•  the ray parameter t,
•  the cylinder hit point, and
•  the surface normal.
5.  The sphere’s hit point, triangle’s hit point, and cylinder hit point each have an associated ray distance t. Chose the point with smallest t, and print one of the following:
•  ray  hits  triangle  ﬁrst
•  ray  hits  sphere  ﬁrst
•  ray  hits  cylinder  ﬁrst
ProgrammingWrite a C++ program using the glmlibrary that writes all the answers to stdout. Use the to_string() function to make printable versions of your vec3, vec4, and mat4 objects.  Each answer should have an output line to identify it.  For example:
std ::cout  <<  "Question  1:\n " ;
std ::cout  <<  "Pixel  in  VCS :    "   <<  glm ::to_string(P_vcs )   <<   "\n " ;
Turn Your Work In
When you are finished, go to mycourses.unh .edu, find assignment 6,click the“Submit”button, and upload ray_cast .cpp.





         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
