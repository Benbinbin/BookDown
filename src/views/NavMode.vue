<template>
  <!-- eslint-disable max-len -->
  <div class="main" :style="{height: pageHeight}">
    <div class="sidebar">
      <div class="nav-top">
        <button class="open" @click="open">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
            <title>在组中打开</title>
            <path d="M6.354 5.5H4a3 3 0 0 0 0 6h3a3 3 0 0 0 2.83-4H9c-.086 0-.17.01-.25.031A2 2 0 0 1 7 10.5H4a2 2 0 1 1 0-4h1.535c.218-.376.495-.714.82-1z" />
            <path d="M9 5.5a3 3 0 0 0-2.83 4h1.098A2 2 0 0 1 9 6.5h3a2 2 0 1 1 0 4h-1.535a4.02 4.02 0 0 1-.82 1H12a3 3 0 1 0 0-6H9z" />
          </svg>
        </button>

        <button class="checked" @click="checked">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
            <title>全选</title>
            <path fill-rule="evenodd" d="M10.854 5.146a.5.5 0 0 1 0 .708l-3 3a.5.5 0 0 1-.708 0l-1.5-1.5a.5.5 0 1 1 .708-.708L7.5 7.793l2.646-2.647a.5.5 0 0 1 .708 0z" />
            <path d="M2 2a2 2 0 0 1 2-2h8a2 2 0 0 1 2 2v13.5a.5.5 0 0 1-.777.416L8 13.101l-5.223 2.815A.5.5 0 0 1 2 15.5V2zm2-1a1 1 0 0 0-1 1v12.566l4.723-2.482a.5.5 0 0 1 .554 0L13 14.566V2a1 1 0 0 0-1-1H4z" />
          </svg>
        </button>

        <button class="unchecked" @click="unchecked">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
            <title>全不选</title>
            <path fill-rule="evenodd" d="M5.5 6.5A.5.5 0 0 1 6 6h4a.5.5 0 0 1 0 1H6a.5.5 0 0 1-.5-.5z" />
            <path d="M2 2a2 2 0 0 1 2-2h8a2 2 0 0 1 2 2v13.5a.5.5 0 0 1-.777.416L8 13.101l-5.223 2.815A.5.5 0 0 1 2 15.5V2zm2-1a1 1 0 0 0-1 1v12.566l4.723-2.482a.5.5 0 0 1 .554 0L13 14.566V2a1 1 0 0 0-1-1H4z" />
          </svg>
        </button>

        <button class="clear" @click="clear('', $event)">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="#ff5959" viewBox="0 0 16 16">
            <title>清空全部</title>
            <path d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0V6z" />
            <path fill-rule="evenodd" d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1v1zM4.118 4L4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4H4.118zM2.5 3V2h11v1h-11z" />
          </svg>
        </button>

        <!-- <button class="more" @click="showMore">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
            <path fill-rule="evenodd" d="M2.5 11.5A.5.5 0 0 1 3 11h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5zm0-4A.5.5 0 0 1 3 7h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5zm0-4A.5.5 0 0 1 3 3h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5z" />
          </svg>
        </button> -->

      </div>
      <div class="pins-list scrollbar" ref="pins">
        <div class="pin" v-for="bookmark of pinsList" :key="bookmark.data.id">
          <input type="checkbox" :value="bookmark" :id="bookmark.data.id" v-model="selectedList">
          <label :for="bookmark.data.id">{{ bookmark.data.title }}</label>
          <button class="clear" @click="clear(bookmark, $event)">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="#ff5959" viewBox="0 0 16 16">
              <title>删除</title>
              <path d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0V6z" />
              <path fill-rule="evenodd" d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1v1zM4.118 4L4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4H4.118zM2.5 3V2h11v1h-11z" />
            </svg>
          </button>
        </div>
      </div>
      <div class="nav-bottom">
        <button class="up" @click="scrollUp('pins')">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
            <path fill-rule="evenodd" d="M7.646 4.646a.5.5 0 0 1 .708 0l6 6a.5.5 0 0 1-.708.708L8 5.707l-5.646 5.647a.5.5 0 0 1-.708-.708l6-6z" />
          </svg>
        </button>

        <button class="sunburst" @click="showNav='sunburst'" v-show="showNav=== null">
          <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="16" height="16" fill="currentColor" viewBox="0 0 32 32">
            <path d="M16 2a1 1 0 0 0-1 1v7.09a5.962 5.962 0 0 0-2.46 1.043L7.838 6.431a1.455 1.455 0 0 0-2.087.024a14.05 14.05 0 0 0 4.054 22.142a10.848 10.848 0 0 0 1.899.768a14.098 14.098 0 0 0 13.844-3.132a1.434 1.434 0 0 0 .028-2.064l-4.699-4.699A5.963 5.963 0 0 0 21.91 17H29a1 1 0 0 0 1-1A14.016 14.016 0 0 0 16 2zm0 10a4 4 0 1 1-4 4a4.005 4.005 0 0 1 4-4zM6.83 8.251l4.296 4.296a5.91 5.91 0 0 0-.011 6.924l-4.277 4.277A12.017 12.017 0 0 1 6.83 8.251zm1.423 16.91l4.276-4.276A5.959 5.959 0 0 0 15 21.91v6.042a11.878 11.878 0 0 1-6.747-2.79zM17 27.956V21.91a5.963 5.963 0 0 0 2.46-1.027l4.283 4.282A11.89 11.89 0 0 1 17 27.956zM21.91 15A6.006 6.006 0 0 0 17 10.09V4.041A12.02 12.02 0 0 1 27.959 15z" />
          </svg>
        </button>

        <button class="down" @click="scrollDown('pins')">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
            <path fill-rule="evenodd" d="M1.646 4.646a.5.5 0 0 1 .708 0L8 10.293l5.646-5.647a.5.5 0 0 1 .708.708l-6 6a.5.5 0 0 1-.708 0l-6-6a.5.5 0 0 1 0-.708z" />
          </svg>
        </button>

      </div>
      <div class="navigator" :class="navSize === 'small' ? 'navigator-small' : 'navigator-large'">
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="#2f89fc" viewBox="0 0 16 16" class="enlarge btn" @click="navSize='large'" v-show="navSize==='small' && showNav==='sunburst'">
          <path fill-rule="evenodd" d="M15 2a1 1 0 0 0-1-1H2a1 1 0 0 0-1 1v12a1 1 0 0 0 1 1h12a1 1 0 0 0 1-1V2zM0 2a2 2 0 0 1 2-2h12a2 2 0 0 1 2 2v12a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2V2zm5.854 8.803a.5.5 0 1 1-.708-.707L9.243 6H6.475a.5.5 0 1 1 0-1h3.975a.5.5 0 0 1 .5.5v3.975a.5.5 0 1 1-1 0V6.707l-4.096 4.096z" />
        </svg>
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="#2f89fc" viewBox="0 0 16 16" class="collapse btn" @click="navSize='small'" v-show="navSize==='large' && showNav==='sunburst'">
          <path fill-rule="evenodd" d="M15 2a1 1 0 0 0-1-1H2a1 1 0 0 0-1 1v12a1 1 0 0 0 1 1h12a1 1 0 0 0 1-1V2zM0 2a2 2 0 0 1 2-2h12a2 2 0 0 1 2 2v12a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2V2zm10.096 3.146a.5.5 0 1 1 .707.708L6.707 9.95h2.768a.5.5 0 1 1 0 1H5.5a.5.5 0 0 1-.5-.5V6.475a.5.5 0 1 1 1 0v2.768l4.096-4.097z" />
        </svg>
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="#ff5959" viewBox="0 0 16 16" class="close btn" :style="{left: leftPos}" v-show="showNav==='sunburst'" @click="closeNav">
          <path d="M14 1a1 1 0 0 1 1 1v12a1 1 0 0 1-1 1H2a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1h12zM2 0a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V2a2 2 0 0 0-2-2H2z" />
          <path d="M4.646 4.646a.5.5 0 0 1 .708 0L8 7.293l2.646-2.647a.5.5 0 0 1 .708.708L8.707 8l2.647 2.646a.5.5 0 0 1-.708.708L8 8.707l-2.646 2.647a.5.5 0 0 1-.708-.708L7.293 8 4.646 5.354a.5.5 0 0 1 0-.708z" />
        </svg>
        <sunburst v-show="showNav==='sunburst'" :size="navSize" :root="root" :select="select" :current="current" @changeSelect="changeSelectHandler" @changeCurrent="changeCurrentHandler"></sunburst>
      </div>
    </div>
    <div class="bookmarks-list">
      <div class="first">
        <div class="folder">
          <p>{{ current.data.title ? current.data.title : '根目录' }}</p>
        </div>
        <ul class="scrollbar" ref="first">
          <li v-for="bookmark of firstBookmarksList" :key="bookmark.data.id" :style="folderStyle(bookmark)" @click="clickHandler(bookmark, 'first', $event)">
            <svg v-if="bookmark.data.children" xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
              <path d="M.54 3.87L.5 3a2 2 0 0 1 2-2h3.672a2 2 0 0 1 1.414.586l.828.828A2 2 0 0 0 9.828 3h3.982a2 2 0 0 1 1.992 2.181l-.637 7A2 2 0 0 1 13.174 14H2.826a2 2 0 0 1-1.991-1.819l-.637-7a1.99 1.99 0 0 1 .342-1.31zM2.19 4a1 1 0 0 0-.996 1.09l.637 7a1 1 0 0 0 .995.91h10.348a1 1 0 0 0 .995-.91l.637-7A1 1 0 0 0 13.81 4H2.19zm4.69-1.707A1 1 0 0 0 6.172 2H2.5a1 1 0 0 0-1 .981l.006.139C1.72 3.042 1.95 3 2.19 3h5.396l-.707-.707z" />
            </svg>
            <svg v-if="!bookmark.data.children" xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bookmark" viewBox="0 0 16 16">
              <path d="M2 2a2 2 0 0 1 2-2h8a2 2 0 0 1 2 2v13.5a.5.5 0 0 1-.777.416L8 13.101l-5.223 2.815A.5.5 0 0 1 2 15.5V2zm2-1a1 1 0 0 0-1 1v12.566l4.723-2.482a.5.5 0 0 1 .554 0L13 14.566V2a1 1 0 0 0-1-1H4z" />
            </svg>
            <span>{{ bookmark.data.title }}</span>
          </li>
        </ul>
        <div class="nav-bottom">
          <button class="back" @click="back" :disabled="!current.parent">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
              <path fill-rule="evenodd" d="M11.354 1.646a.5.5 0 0 1 0 .708L5.707 8l5.647 5.646a.5.5 0 0 1-.708.708l-6-6a.5.5 0 0 1 0-.708l6-6a.5.5 0 0 1 .708 0z" />
            </svg>
          </button>

          <button class="up" @click="scrollUp('first')">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
              <path fill-rule="evenodd" d="M7.646 4.646a.5.5 0 0 1 .708 0l6 6a.5.5 0 0 1-.708.708L8 5.707l-5.646 5.647a.5.5 0 0 1-.708-.708l6-6z" />
            </svg>
          </button>
          <button class="down" @click="scrollDown('first')">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
              <path fill-rule="evenodd" d="M1.646 4.646a.5.5 0 0 1 .708 0L8 10.293l5.646-5.647a.5.5 0 0 1 .708.708l-6 6a.5.5 0 0 1-.708 0l-6-6a.5.5 0 0 1 0-.708z" />
            </svg>
          </button>

        </div>
      </div>

      <div class="second">
        <div class="folder">
          <p>{{ select ? select.data.title : '' }}</p>
        </div>
        <ul class="scrollbar" ref="second">
          <li v-for="bookmark of secondBookmarksList" :key="bookmark.data.id" :style="folderStyle(bookmark)" @click="clickHandler(bookmark, 'second', $event)">
            <svg v-if="bookmark.data.children" xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
              <path d="M.54 3.87L.5 3a2 2 0 0 1 2-2h3.672a2 2 0 0 1 1.414.586l.828.828A2 2 0 0 0 9.828 3h3.982a2 2 0 0 1 1.992 2.181l-.637 7A2 2 0 0 1 13.174 14H2.826a2 2 0 0 1-1.991-1.819l-.637-7a1.99 1.99 0 0 1 .342-1.31zM2.19 4a1 1 0 0 0-.996 1.09l.637 7a1 1 0 0 0 .995.91h10.348a1 1 0 0 0 .995-.91l.637-7A1 1 0 0 0 13.81 4H2.19zm4.69-1.707A1 1 0 0 0 6.172 2H2.5a1 1 0 0 0-1 .981l.006.139C1.72 3.042 1.95 3 2.19 3h5.396l-.707-.707z" />
            </svg>
            <svg v-if="!bookmark.data.children" xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bookmark" viewBox="0 0 16 16">
              <path d="M2 2a2 2 0 0 1 2-2h8a2 2 0 0 1 2 2v13.5a.5.5 0 0 1-.777.416L8 13.101l-5.223 2.815A.5.5 0 0 1 2 15.5V2zm2-1a1 1 0 0 0-1 1v12.566l4.723-2.482a.5.5 0 0 1 .554 0L13 14.566V2a1 1 0 0 0-1-1H4z" />
            </svg>
            <span>{{ bookmark.data.title }}</span>
          </li>
        </ul>
        <div class="nav-bottom">
          <button class="up" @click="scrollUp('second')">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
              <path fill-rule="evenodd" d="M7.646 4.646a.5.5 0 0 1 .708 0l6 6a.5.5 0 0 1-.708.708L8 5.707l-5.646 5.647a.5.5 0 0 1-.708-.708l6-6z" />
            </svg>
          </button>
          <button class="down" @click="scrollDown('second')">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
              <path fill-rule="evenodd" d="M1.646 4.646a.5.5 0 0 1 .708 0L8 10.293l5.646-5.647a.5.5 0 0 1 .708.708l-6 6a.5.5 0 0 1-.708 0l-6-6a.5.5 0 0 1 0-.708z" />
            </svg>
          </button>

        </div>
      </div>

    </div>
  </div>
</template>

<script>
import * as d3 from 'd3';
import Sunburst from '@/components/Sunburst.vue';

export default {
  name: 'Nav',
  components: {
    Sunburst,
  },
  props: ['bookmarks', 'previewMode'],
  data() {
    return {
      pageHeight: '500px',
      root: null,
      current: null,
      select: null,
      set: new Set(),
      pinsList: [],
      selectedList: [],
      showNav: 'sunburst',
      navSize: 'small',
      showMore: false,
    };
  },
  computed: {
    leftPos() {
      if (this.navSize === 'small') return 0;
      return '10px';
    },
    firstBookmarksList() {
      if (!this.current) return [];
      return this.current.children;
    },
    secondBookmarksList() {
      if (!this.select) return [];
      return this.select.children;
    },
  },
  methods: {
    getStorage() {
      return new Promise((resolve, reject) => {
        chrome.storage.local.get(['width', 'height', 'mode'], (data) => {
          resolve(data);
        });
      });
    },
    folderStyle(node) {
      if (node === this.select) {
        return {
          border: '3px solid #2f89fc',
          background: '#2f89fc',
          color: '#f5f5f5',
        };
      }
      if (node.height !== 0) {
        return {
          border: '3px solid #2f89fc',
        };
      }
      //   叶子节点无样式
      return 'none';
    },
    changeSelectHandler(node) {
      this.select = node;
    },
    changeCurrentHandler(node) {
      this.current = node;
    },
    open() {
      const promises = [];
      this.selectedList.forEach((node) => {
        const p = this.openUrl(node.data.url, 'multi');
        promises.push(p);
      });
      // console.log(this.selectedList);
      Promise.all(promises).then((tabs) => {
        const tabIds = tabs.map((item) => item.id);
        chrome.tabs.group({
          tabIds,
        });
      });
      const arr = this.selectedList.slice();

      arr.forEach((item) => {
        this.clear(item);
      });
    },
    checked() {
      this.selectedList = this.pinsList;
    },
    clear(node) {
      if (node) {
        this.set.delete(node);
        const pinIndex = this.pinsList.indexOf(node);
        const selectIndex = this.selectedList.indexOf(node);
        this.pinsList.splice(pinIndex, 1);
        if (selectIndex !== -1) this.selectedList.splice(selectIndex, 1);
      } else {
        this.set.clear();
        this.pinsList = [];
        this.selectedList = [];
      }
    },
    unchecked() {
      this.selectedList = [];
    },
    closeNav() {
      this.showNav = null;
      this.navSize = 'small';
    },
    scrollUp(val) {
      this.$refs[val].scrollTop = 0;
    },
    scrollDown(val) {
      this.$refs[val].scrollTop = this.$refs[val].scrollHeight;
    },
    back() {
      this.current = this.current.parent;
      this.select = null;
    },
    getCurrentTab() {
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
    // eslint-disable-next-line consistent-return
    openUrl(url, mode = this.previewMode) {
      if (mode === 'default') {
        return new Promise((resolve, reject) => {
          this.getCurrentTab().then((tab) => {
            chrome.tabs.create({
              active: false,
              url: tab.url,
            });

            chrome.tabs.update({ url }, (t) => resolve(t));
          });
        });
      }
      if (mode === 'one') {
        return new Promise((resolve, reject) => {
          chrome.tabs.update({ url }, (t) => resolve(t));
        });
      }
      if (mode === 'multi') {
        return new Promise((resolve, reject) => {
          chrome.tabs.create(
            {
              active: false,
              url,
            },
            (t) => resolve(t),
          );
        });
      }
    },
    clickHandler(node, column, event) {
      // console.log(event);
      if (event.ctrlKey && !node.data.children) {
        // 按住 Ctrl 键点击书签
        if (this.set.has(node)) return;
        this.set.add(node);
        this.selectedList.push(node);
        this.pinsList.push(node);
        return;
      }
      if (column === 'first') {
        // 点击第一列的文件夹，「展开」到第二列
        if (node.data.children) {
          this.select = node;
        } else {
          // 点击第一列的书签
          this.openUrl(node.data.url);
        }
      } else if (node.data.children) {
        // 点击第二列的文件夹，切换第一列和第二列，下钻「展开」
        this.current = this.select;
        this.select = node;
      } else {
        // 点击第二列的书签
        this.openUrl(node.data.url);
      }
    },
  },
  created() {
    this.getStorage().then((data) => {
      this.pageHeight = `${data.height}px`;
      // this.treeWeight = `${data.width}px`;
    });
    // 结构化数据
    this.root = d3.hierarchy(this.bookmarks).eachAfter((d) => {
      if (d.height === 0) {
        d.value = 0;
      } else if (d.height === 1) {
        d.value = 1;
      } else {
        let value = 0;

        d.children.forEach((item) => {
          value += item.value;
        });
        d.value = value;
      }
    });
    // .sort((a, b) => b.value - a.value);

    // console.log(this.root);
    // 计算节点的层次布局
    const tree = d3.partition().size([2 * Math.PI, this.root.height + 1])(
      this.root,
    );

    tree.each((d) => {
      d.current = {
        x0: d.x0,
        x1: d.x1,
        y0: d.y0,
        y1: d.y1,
      };
    });

    this.current = this.root;
  },
};
</script>

<style lang="scss" scoped>
input:focus,
button:focus {
  outline: none;
}

.main {
  // height: 500px;
  width: 100%;
  // border: 1px solid $blue;
  display: grid;
  position: relative;
  grid-template-columns: 30% minmax(0, 1fr);
  grid-template-areas: "pins bookmarks";

  li,
  label {
    margin: 0.25rem auto;
    text-align: center;
    overflow: hidden;
    border-radius: 0.3rem;
    cursor: pointer;
  }

  // 定制滚动条
  .scrollbar::-webkit-scrollbar {
    width: 2px;
  }
  // 滚动条的内层滑块颜色
  .scrollbar::-webkit-scrollbar-thumb {
    background-color: $light-bg;
  }
  // 隐藏滑轨两头的监听按钮
  .scrollbar::-webkit-scrollbar-button {
    display: none;
  }

  .nav-top,
  .nav-bottom {
    height: 25px;
    display: flex;
    align-items: center;
    button {
      width: 100%;
      height: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
      background: $light;
      border: none;
      padding: 2px 0;
      cursor: pointer;

      &:hover {
        background: $blue;
        color: $light;
      }
    }
  }

  .sidebar {
    height: inherit;
    width: 100%;
    border-right: 2px solid $light;
    grid-area: pins;
    display: flex;
    flex-direction: column;

    .nav-top {
      border-bottom: 2px solid $light-bg;
    }

    .navigator {
      width: 100%;

      .btn {
        cursor: pointer;
        position: absolute;
      }

      .enlarge {
        top: 0;
        right: 0;
      }

      .collapse {
        top: 0;
        right: 10px;
      }

      .close {
        top: 0;
      }

      .sunburst {
        bottom: 0;
        left: 10px;
      }
    }

    .navigator-small {
      position: relative;
      background: $light-bg;
    }

    .navigator-large {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(235, 235, 235, 0.8);
    }

    .pins-list {
      padding: 5px;
      flex-grow: 1;
      overflow-y: auto;
      scroll-behavior: smooth;

      .pin {
        margin: 0.25rem 0;
        width: 100%;
        display: flex;
        justify-content: space-between;
        align-items: center;
        label {
          width: 100%;
          padding: 0.25rem;
          margin: 0 0.25rem;
          border: 1px solid $yellow;
          border-left: 5px solid $yellow;
          white-space: nowrap;
          overflow: hidden;
          text-overflow: ellipsis;
          user-select: none;

          &:hover {
            background: $yellow;
            color: $light;
            font-weight: bold;
          }
        }
        button {
          display: flex;
          justify-content: center;
          align-items: center;
          cursor: pointer;
          background: none;
          border: none;
        }
      }
    }
  }
  .bookmarks-list {
    height: inherit;
    grid-area: bookmarks;
    display: grid;
    grid-template-columns: 50% 50%;
    grid-template-areas: "first second";

    .first {
      display: flex;
      flex-direction: column;
      height: inherit;
      grid-area: first;
    }
    .second {
      display: flex;
      flex-direction: column;
      height: inherit;
      grid-area: second;
    }

    .folder {
      width: 100%;
      height: 25px;
      background: $light;
      border-bottom: 2px solid $light-bg;
      p {
        height: 100%;
        line-height: 25px;
        font-size: 12px;
        text-align: center;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
      }
    }

    ul {
      height: 100%;
      overflow-y: auto;
      padding: 0 5px;
      scroll-behavior: smooth;

      li {
        padding: 0.5rem;
        list-style: none;
        border: 1px solid $light-bg;
        background: $light;
        display: flex;
        justify-content: space-between;
        align-items: center;
        svg {
          width: 16px;
        }
        span {
          padding-left: 0.5rem;
          width: 100%;
          white-space: nowrap;
          overflow: hidden;
          text-overflow: ellipsis;
        }

        &:hover {
          background: $blue;
          color: $light;
          //   font-weight: bold;
        }
      }
    }
  }
}
</style>
