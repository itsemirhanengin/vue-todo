<script>
  export default {
    name: 'App',
    data() {
      return {
        label: '',
        items: [],
      };
    },
    methods: {
      add(e) {
        e.preventDefault();
        
        this.items.push({
          label: this.label,
          closed: false,
        });
        this.label = '';
      },
      remove(index) {
        this.items.splice(index, 1);
      },
      close(index) {
        const item = this.items[index];
        item.closed = !item.closed;
      }
    },
  }
</script>

<template>
  <div id="app">
    <div class="container">
      <ul>
        <li class="not-found" v-if="items.length === 0">No items found.</li>
        <li :class="`item${item.closed ? ' closed' : ''}`" v-for="(item, index) in items" :key="item.label">
          {{item.label}}
          <div class="actions">
            <button class="close" @click="close(index)">√</button>
            <button class="remove" @click="remove(index)">x</button>
          </div>
        </li>
      </ul>

      <form @submit="add">
        <input
          type="text"
          placeholder="What do you want to finish today?"
          v-model="label"
        />
        <button type="submit">Add!</button>
      </form>
    </div>
  </div>
</template>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');

  * {
    margin: 0;
    padding: 0;
  }

  ul {
    list-style: none;
  }

  .container {
    width: 50%;
    margin-left: auto;
    margin-right: auto;
    border: 1px solid rgba(0,0,0,.2);
    border-radius: 6px;
    padding: 20px;
    margin-top: 100px;
  }

  .not-found {
    background-color: rgb(201, 201, 201);
    color: #333;
    padding: 12px 16px;
    border-radius: 4px;
    font-family: 'Roboto', sans-serif;
    font-size: 14px;
  }
  .item {
    background-color: rgb(235, 235, 235);
    color: #333;
    padding: 12px 16px;
    border-radius: 4px;
    font-family: 'Roboto', sans-serif;
    font-size: 14px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .item.closed {
    text-decoration: line-through;
  }
  .item:not(:last-child) {
    margin-bottom: 8px;
  }
  .item button.remove {
    width: 40px;
    height: 40px;
    background-color: rgba(182, 21, 0, 0.911);
    color: #fff;
    cursor: pointer;
    border: 0;
    border-radius: 6px;
    font-size: 18px;
    margin-left: 10px;
  }
  .item button.close {
    width: 40px;
    height: 40px;
    background-color: rgba(67, 182, 0, 0.911);
    color: #fff;
    cursor: pointer;
    border: 0;
    border-radius: 6px;
    font-size: 18px;
  }

  form {
    display: flex;
    margin-top: 20px;
  }
  form input {
    width: 100%;
    border-top-left-radius: 6px;
    border-bottom-left-radius: 6px;
    border-top-right-radius: 0;
    border-bottom-right-radius: 0;
    border: 2px solid #000;
    border-right: 0;
    padding: 0 12px;
    font-size: 14px;
  }
  form input:focus {
    outline: none;
  }
  form input::placeholder {
    color: #000;
  }
  form button {
    flex-shrink: 0;
    height: 40px;
    padding: 0 16px;
    border-top-left-radius: 0;
    border-bottom-left-radius: 0;
    border-top-right-radius: 6px;
    border-bottom-right-radius: 6px;
    border: 0;
    background-color: #000;
    color: #fff;
    cursor: pointer;
  }

  form button:disabled {
    cursor: not-allowed;
    opacity: .3;
  }
</style>
