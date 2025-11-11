### **1. Percentage Calculation**

css

/* % LUÔN tính dựa trên PARENT ELEMENT */
.parent { width: 50%; }     /* 50% của parent's parent */
.child { width: 50%; }      /* 50% của .parent */

### **2. Containing Block Concept**

css

/* QUAN TRỌNG: "Containing Block" xác định % tính theo đâu */
.element { width: 50%; }    /* 50% của Containing Block */