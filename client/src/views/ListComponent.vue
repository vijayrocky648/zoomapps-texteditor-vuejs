<template>
    <div class="list-container">
        <h1>Enter Your Zoom ID</h1>
        <input v-model="newItemId" @input="validateInput"  placeholder="Enter an ID">
        <button @click="addItem">Add Item</button>
        <ul>
            <li v-for="(item, index) in items" :key="index">
                {{ item.id }}
                <button @click="deleteItem(index)">Delete</button>
            </li>
        </ul>
        <div>
            <p style="color: red;font-weight: bolder;">Please note that the Zoom ID entered here should pertain to a
                technical or business-related conversation. We are storing this data in a centralized system </p>
        </div>
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            newItemId: '',
            items: [],
        };
    },
    methods: {
        validateInput() {
            this.newItemId = this.newItemId.replace(/[^0-9]/g, '');
        },
        addItem() {
            if (this.newItemId) {
                this.items.push({ id: this.newItemId });
                this.newItemId = '';
                this.saveData();
            }
        },
        deleteItem(index) {
            this.items.splice(index, 1);
            this.saveData();
        },
        saveData() {
            // Save the data to the JSON file (data.json)
            fetch('/data.json', {
                method: 'PUT',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify(this.items),
            });
        },
        fetchData() {
            // Fetch the data from the JSON file (data.json)
            fetch('./data.json')
                .then((response) => response.json())
                .then((data) => {
                    this.items = data;
                });
        },
    },
    mounted() {
        // Load data when the component is mounted
        this.fetchData();
    },
};
</script>
<style scoped>
.list-container {
    max-width: 400px;
    margin: 0 auto;
    padding: 20px;
    background-color: #f5f5f5;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h1 {
    font-size: 24px;
    margin-bottom: 20px;
    color: #333;
    text-align: center;
}

input {
    width: 100%;
    padding: 10px;
    margin-bottom: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
}

button {
    background-color: #007BFF;
    color: #fff;
    border: none;
    border-radius: 5px;
    padding: 10px 20px;
    cursor: pointer;
    width: 100%;
}

button:hover {
    background-color: #0056b3;
}

ul {
    list-style: none;
    padding: 0;
}

li {
    background-color: #fff;
    padding: 10px;
    margin: 5px 0;
    border: 1px solid #ccc;
    border-radius: 5px;
    display: flex;
    justify-content: space-between;
}

li button {
    background-color: #ff6b6b;
    color: #fff;
    border: none;
    border-radius: 5px;
    padding: 5px 10px;
    cursor: pointer;
    width: 20%;
}

li button:hover {
    background-color: #d9534f;
}
</style>
