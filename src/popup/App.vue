<template>
  <!-- eslint-disable max-len -->
  <div>
    <div class="btn-container" v-if="currentTab === 'buttons'">
      <!-- <button class="btn" @click="addBookmark" v-if="!booked">
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
          <path fill-rule="evenodd" d="M8 4a.5.5 0 0 1 .5.5V6H10a.5.5 0 0 1 0 1H8.5v1.5a.5.5 0 0 1-1 0V7H6a.5.5 0 0 1 0-1h1.5V4.5A.5.5 0 0 1 8 4z" />
          <path d="M2 2a2 2 0 0 1 2-2h8a2 2 0 0 1 2 2v13.5a.5.5 0 0 1-.777.416L8 13.101l-5.223 2.815A.5.5 0 0 1 2 15.5V2zm2-1a1 1 0 0 0-1 1v12.566l4.723-2.482a.5.5 0 0 1 .554 0L13 14.566V2a1 1 0 0 0-1-1H4z" />
        </svg>
        <span>添加书签</span>
      </button>
      <div v-if="booked" @mouseenter="editing=true" @mouseleave="editing=false">
        <button class="btn-success" v-show="!editing">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
            <path fill-rule="evenodd" d="M10.854 5.146a.5.5 0 0 1 0 .708l-3 3a.5.5 0 0 1-.708 0l-1.5-1.5a.5.5 0 1 1 .708-.708L7.5 7.793l2.646-2.647a.5.5 0 0 1 .708 0z" />
            <path d="M2 2a2 2 0 0 1 2-2h8a2 2 0 0 1 2 2v13.5a.5.5 0 0 1-.777.416L8 13.101l-5.223 2.815A.5.5 0 0 1 2 15.5V2zm2-1a1 1 0 0 0-1 1v12.566l4.723-2.482a.5.5 0 0 1 .554 0L13 14.566V2a1 1 0 0 0-1-1H4z" />
          </svg>
          <span>已添加</span>
        </button>
        <div v-show="editing" class="edit-buttons-container">
          <button class="btn-delete" @click="deleteBookmark">删除</button>
          <button class="btn-edit">编辑</button>
        </div>
      </div> -->

      <button class="btn" @click="getBookmarks">
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16" style="transform: rotate(-90deg)">
          <path fill-rule="evenodd" d="M6 3.5A1.5 1.5 0 0 1 7.5 2h1A1.5 1.5 0 0 1 10 3.5v1A1.5 1.5 0 0 1 8.5 6v1H14a.5.5 0 0 1 .5.5v1a.5.5 0 0 1-1 0V8h-5v.5a.5.5 0 0 1-1 0V8h-5v.5a.5.5 0 0 1-1 0v-1A.5.5 0 0 1 2 7h5.5V6A1.5 1.5 0 0 1 6 4.5v-1zM8.5 5a.5.5 0 0 0 .5-.5v-1a.5.5 0 0 0-.5-.5h-1a.5.5 0 0 0-.5.5v1a.5.5 0 0 0 .5.5h1zM0 11.5A1.5 1.5 0 0 1 1.5 10h1A1.5 1.5 0 0 1 4 11.5v1A1.5 1.5 0 0 1 2.5 14h-1A1.5 1.5 0 0 1 0 12.5v-1zm1.5-.5a.5.5 0 0 0-.5.5v1a.5.5 0 0 0 .5.5h1a.5.5 0 0 0 .5-.5v-1a.5.5 0 0 0-.5-.5h-1zm4.5.5A1.5 1.5 0 0 1 7.5 10h1a1.5 1.5 0 0 1 1.5 1.5v1A1.5 1.5 0 0 1 8.5 14h-1A1.5 1.5 0 0 1 6 12.5v-1zm1.5-.5a.5.5 0 0 0-.5.5v1a.5.5 0 0 0 .5.5h1a.5.5 0 0 0 .5-.5v-1a.5.5 0 0 0-.5-.5h-1zm4.5.5a1.5 1.5 0 0 1 1.5-1.5h1a1.5 1.5 0 0 1 1.5 1.5v1a1.5 1.5 0 0 1-1.5 1.5h-1a1.5 1.5 0 0 1-1.5-1.5v-1zm1.5-.5a.5.5 0 0 0-.5.5v1a.5.5 0 0 0 .5.5h1a.5.5 0 0 0 .5-.5v-1a.5.5 0 0 0-.5-.5h-1z" />
        </svg>
        <span>浏览书签</span>
      </button>
      <button class="btn" @click="openTab('bookmarksManager')">
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
          <path fill-rule="evenodd" d="M6 8V1h1v6.117L8.743 6.07a.5.5 0 0 1 .514 0L11 7.117V1h1v7a.5.5 0 0 1-.757.429L9 7.083 6.757 8.43A.5.5 0 0 1 6 8z" />
          <path d="M3 0h10a2 2 0 0 1 2 2v12a2 2 0 0 1-2 2H3a2 2 0 0 1-2-2v-1h1v1a1 1 0 0 0 1 1h10a1 1 0 0 0 1-1V2a1 1 0 0 0-1-1H3a1 1 0 0 0-1 1v1H1V2a2 2 0 0 1 2-2z" />
          <path d="M1 5v-.5a.5.5 0 0 1 1 0V5h.5a.5.5 0 0 1 0 1h-2a.5.5 0 0 1 0-1H1zm0 3v-.5a.5.5 0 0 1 1 0V8h.5a.5.5 0 0 1 0 1h-2a.5.5 0 0 1 0-1H1zm0 3v-.5a.5.5 0 0 1 1 0v.5h.5a.5.5 0 0 1 0 1h-2a.5.5 0 0 1 0-1H1z" />
        </svg>
        <span>书签管理</span>
      </button>
      <button class="btn" @click="openTab('optionPage')">
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
          <path fill-rule="evenodd" d="M11.5 2a1.5 1.5 0 1 0 0 3 1.5 1.5 0 0 0 0-3zM9.05 3a2.5 2.5 0 0 1 4.9 0H16v1h-2.05a2.5 2.5 0 0 1-4.9 0H0V3h9.05zM4.5 7a1.5 1.5 0 1 0 0 3 1.5 1.5 0 0 0 0-3zM2.05 8a2.5 2.5 0 0 1 4.9 0H16v1H6.95a2.5 2.5 0 0 1-4.9 0H0V8h2.05zm9.45 4a1.5 1.5 0 1 0 0 3 1.5 1.5 0 0 0 0-3zm-2.45 1a2.5 2.5 0 0 1 4.9 0H16v1h-2.05a2.5 2.5 0 0 1-4.9 0H0v-1h9.05z" />
        </svg>
        <span>设置参数</span>
      </button>
    </div>
    <div class="bookmarks-container" v-if="currentTab === 'bookmarks'" :style="{width: popupWidth}">
      <ul class="navbar">
        <li @click="currentTab='buttons'">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
            <title>返回</title>
            <path fill-rule="evenodd" d="M15 2a1 1 0 0 0-1-1H2a1 1 0 0 0-1 1v12a1 1 0 0 0 1 1h12a1 1 0 0 0 1-1V2zM0 2a2 2 0 0 1 2-2h12a2 2 0 0 1 2 2v12a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2V2zm11.5 5.5a.5.5 0 0 1 0 1H5.707l2.147 2.146a.5.5 0 0 1-.708.708l-3-3a.5.5 0 0 1 0-.708l3-3a.5.5 0 1 1 .708.708L5.707 7.5H11.5z" />
          </svg>
        </li>
        <li v-show="mode==='nav'" @click="mode='tree'">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
            <title>导航器模式</title>
            <path d="M2.5 4a.5.5 0 1 0 0-1 .5.5 0 0 0 0 1zm2-.5a.5.5 0 1 1-1 0 .5.5 0 0 1 1 0zm1 .5a.5.5 0 1 0 0-1 .5.5 0 0 0 0 1z" />
            <path d="M2 1a2 2 0 0 0-2 2v10a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V3a2 2 0 0 0-2-2H2zm12 1a1 1 0 0 1 1 1v2H1V3a1 1 0 0 1 1-1h12zM1 13V6h4v8H2a1 1 0 0 1-1-1zm5 1V6h9v7a1 1 0 0 1-1 1H6z" />
          </svg>
        </li>
        <li v-show="mode==='tree'" @click="mode='nav'">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16" style="transform: rotate(-90deg)">
            <title>树图模式</title>
            <path fill-rule="evenodd" d="M6 3.5A1.5 1.5 0 0 1 7.5 2h1A1.5 1.5 0 0 1 10 3.5v1A1.5 1.5 0 0 1 8.5 6v1H14a.5.5 0 0 1 .5.5v1a.5.5 0 0 1-1 0V8h-5v.5a.5.5 0 0 1-1 0V8h-5v.5a.5.5 0 0 1-1 0v-1A.5.5 0 0 1 2 7h5.5V6A1.5 1.5 0 0 1 6 4.5v-1zM8.5 5a.5.5 0 0 0 .5-.5v-1a.5.5 0 0 0-.5-.5h-1a.5.5 0 0 0-.5.5v1a.5.5 0 0 0 .5.5h1zM0 11.5A1.5 1.5 0 0 1 1.5 10h1A1.5 1.5 0 0 1 4 11.5v1A1.5 1.5 0 0 1 2.5 14h-1A1.5 1.5 0 0 1 0 12.5v-1zm1.5-.5a.5.5 0 0 0-.5.5v1a.5.5 0 0 0 .5.5h1a.5.5 0 0 0 .5-.5v-1a.5.5 0 0 0-.5-.5h-1zm4.5.5A1.5 1.5 0 0 1 7.5 10h1a1.5 1.5 0 0 1 1.5 1.5v1A1.5 1.5 0 0 1 8.5 14h-1A1.5 1.5 0 0 1 6 12.5v-1zm1.5-.5a.5.5 0 0 0-.5.5v1a.5.5 0 0 0 .5.5h1a.5.5 0 0 0 .5-.5v-1a.5.5 0 0 0-.5-.5h-1zm4.5.5a1.5 1.5 0 0 1 1.5-1.5h1a1.5 1.5 0 0 1 1.5 1.5v1a1.5 1.5 0 0 1-1.5 1.5h-1a1.5 1.5 0 0 1-1.5-1.5v-1zm1.5-.5a.5.5 0 0 0-.5.5v1a.5.5 0 0 0 .5.5h1a.5.5 0 0 0 .5-.5v-1a.5.5 0 0 0-.5-.5h-1z" />
          </svg>
        </li>
        <li @click="showMore=true" v-show="!showMore">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
            <title>更多</title>
            <path fill-rule="evenodd" d="M2.5 11.5A.5.5 0 0 1 3 11h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5zm0-4A.5.5 0 0 1 3 7h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5zm0-4A.5.5 0 0 1 3 3h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5z" />
          </svg>
        </li>
        <li @click="showMore=false" v-show="showMore">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="#ff5959" viewBox="0 0 16 16">
            <title>关闭</title>
            <path d="M4.646 4.646a.5.5 0 0 1 .708 0L8 7.293l2.646-2.647a.5.5 0 0 1 .708.708L8.707 8l2.647 2.646a.5.5 0 0 1-.708.708L8 8.707l-2.646 2.647a.5.5 0 0 1-.708-.708L7.293 8 4.646 5.354a.5.5 0 0 1 0-.708z" />
          </svg>
        </li>
      </ul>
      <ul class="more-btns" v-show="showMore">
        <li class="preview-btn" @click="showMore = false">
          <ul>
            <li>
              <input type="radio" id="default" name="default" value="default" v-model="previewMode">
              <label for="default">默认</label>
            </li>
            <li>
              <input type="radio" id="one" name="one" value="one" v-model="previewMode">
              <label for="one">预览模式</label>
            </li>
            <li>
              <input type="radio" id="multi" name="multi" value="multi" v-model="previewMode">
              <label for="multi">后台模式</label>
            </li>
          </ul>
        </li>
        <!-- <li class="enlarge-btn" @click="enlarge">
          最大化
        </li> -->
      </ul>
      <tree v-if="mode === 'tree'" :bookmarks="bookmarks" :previewMode="previewMode" class="tree"></tree>
      <!-- <tree-mode v-if="mode === 'tree'" :bookmarks="bookmarks" :previewMode="previewMode" class="tree"></tree-mode> -->
      <nav-mode v-if="mode==='nav'" :bookmarks="bookmarks" :previewMode="previewMode"></nav-mode>
    </div>
  </div>
</template>

<script>
import Tree from '@/components/Tree.vue';
// import TreeMode from '@/views/TreeMode.vue';
import NavMode from '@/views/NavMode.vue';

export default {
  name: 'App',
  components: {
    Tree,
    // TreeMode,
    NavMode,
  },
  data() {
    return {
      id: null,
      popupWidth: '500px',
      booked: false,
      editing: false,
      currentTab: 'buttons',
      bookmarks: [],
      mode: 'nav',
      showMore: false,
      previewMode: 'default',
    };
  },

  methods: {
    getStorage() {
      return new Promise((resolve, reject) => {
        chrome.storage.local.get(['width', 'height', 'mode'], (data) => {
          resolve(data);
        });
      });
    },
    enlarge() {
      this.showMore = false;
    },
    getTab() {
      return new Promise((resolve, reject) => {
        chrome.tabs.query(
          {
            active: true,
            currentWindow: true,
          },
          (tabs) => {
            resolve(tabs[0]);
          },
        );
      });
    },
    searchBookmark(query) {
      return new Promise((resolve, reject) => {
        chrome.bookmarks.search(query, (bookmarkNode) => {
          resolve(bookmarkNode);
        });
      });
    },
    addBookmark() {
      this.getTab().then((tab) => {
        // console.log(tab.title);
        console.log(tab.url);
        chrome.bookmarks.create(
          {
            title: tab.title,
            url: tab.url,
          },
          (bookmarkNode) => {
            // console.log(bookmarkNode);
            this.id = bookmarkNode.id;
            this.booked = true;
          },
        );
      });
    },
    deleteBookmark() {
      chrome.bookmarks.remove(this.id, () => {
        this.id = null;
        this.booked = false;
        // console.log('deleted');
      });
    },
    getTree() {
      return new Promise((resolve, reject) => {
        chrome.bookmarks.getTree((bookmarks) => resolve(bookmarks));
      });
    },
    getBookmarks() {
      this.getTree().then((bookmarks) => {
        // console.log(bookmarks);
        [this.bookmarks] = bookmarks;
        this.currentTab = 'bookmarks';
      });
    },
    openTab(target) {
      let url = '';
      if (target === 'bookmarksManager') {
        url = 'chrome://bookmarks/';
      } else if (target === 'optionPage') {
        const { id } = chrome.runtime;
        url = `chrome-extension://${id}/options.html`;
      }
      return new Promise((resolve, reject) => {
        chrome.tabs.create(
          {
            url,
          },
          (t) => resolve(t),
        );
      });
    },
  },
  mounted() {
    this.getTab()
      .then((tab) => {
        const query = {
          url: tab.url,
        };
        return this.searchBookmark(query);
      })
      .then((bookmarkNode) => {
        if (!bookmarkNode.length) return;
        this.id = bookmarkNode[0].id;
        this.booked = true;
      });

    // chrome.bookmarks.getChildren('0', (bookmarks) => {
    //   console.log(bookmarks);
    // });
  },
  created() {
    this.getStorage().then((data) => {
      this.popupWidth = `${data.width}px`;
      this.mode = data.mode;
    });
  },
};
</script>

<style lang="scss" scoped>
input:focus,
button:focus {
  outline: none;
}

.btn-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;

  button {
    padding: 0.5rem;
    margin: 0.5rem;
    display: flex;
    align-items: center;
    justify-content: space-evenly;
    border-radius: 0.5rem;
    cursor: pointer;
  }

  .btn {
    width: 130px;
    border: 2px solid $blue;
    background: $light;
    color: $dark;
    &:hover {
      background: $blue;
      color: $light;
      font-weight: bold;
    }
  }

  .edit-buttons-container {
    width: 130px;
    display: flex;
    align-items: center;
  }

  .btn-success {
    width: 130px;
    border: 2px solid $green;
    background: $green;
  }

  .btn-delete {
    width: 100%;
    margin-left: 0;
    margin-right: 0;
    border: 2px solid $red;
    border-radius: 0.5rem 0 0 0.5rem;
    background: $red;
    color: $light;
    font-weight: bold;
  }

  .btn-edit {
    width: 100%;
    margin-left: 0;
    margin-right: 0;
    border: 2px solid $blue;
    border-radius: 0 0.5rem 0.5rem 0;
    background: $blue;
    color: $light;
    font-weight: bold;
  }
}

.bookmarks-container {
  // width: 500px;
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;

  li {
    list-style: none;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .navbar {
    width: 100%;
    height: 30px;
    padding: 5px 10px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: $light-bg;
  }

  .more-btns {
    position: absolute;
    z-index: 1;
    right: 10px;
    top: 30px;
    width: 120px;
    display: flex;
    flex-direction: column;
    padding: 10px;
    border: 2px solid $light-bg;
    border-radius: 0.5rem;
    background: rgba(245, 245, 245, 0.8);
    box-shadow: 3px 3px 10px 0px rgba(64, 81, 78, 0.75);

    li {
      width: 100%;
      padding: 5px 0;
      margin: 3px 0;
      border-radius: 0.3rem;
      border: 1px solid $light-bg;
      background: #fff;
      cursor: pointer;
    }

    .preview-btn {
      justify-content: space-around;
      ul {
        width: 100%;
        padding: 0 10px;
        li {
          display: flex;
          justify-content: flex-start;
          border: none;
        }
      }
      input,
      label {
        cursor: pointer;
        margin-left: 5px;
        user-select: none;
      }
    }

    .enlarge-btn:hover {
      background: $blue;
      color: $light;
      font-weight: bold;
    }
  }
}
</style>
