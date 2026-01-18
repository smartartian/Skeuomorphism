<template>
  <div class="app-container">
    <!-- 顶部菜单 Header -->
    <header class="top-header">
      <div class="header-content">
        <div class="logo">Skeuomorphism 拟物化配置 <span class="logo-subtitle">by Element Plus</span></div>

        <el-menu
          :default-active="activeTopMenu"
          mode="horizontal"
          :ellipsis="false"
          @select="handleTopMenuSelect"
          class="top-menu"
        >
          <el-menu-item index="home">说明</el-menu-item>
          <el-menu-item index="components">组件</el-menu-item>
        </el-menu>
        <div class="menu-extra">
          <a href="https://smartartian.github.io/smartisan-icon/" target="_blank" class="external-link">Smartisan Icons</a>
          <div class="version-info">v1.0.0</div>
        </div>
      </div>
    </header>

    <div class="components-demo-layout">
      <!-- 侧边栏 (仅在 activePage === 'demo' 时显示) -->
      <aside class="sidebar" v-show="activePage === 'demo'">
        <div class="sidebar-menu">
          <div 
            v-for="item in menuItems" 
            :key="item.id"
            class="menu-item"
            :class="{ active: activeSection === item.id }"
            @click="scrollToSection(item.id)"
          >
            {{ item.title }}
          </div>
        </div>
      </aside>

      <!-- 主内容区 -->
      <main class="main-content">
      <!-- 演示页面内容 -->
      <el-space v-show="activePage === 'demo'" direction="vertical" :size="20" fill style="width: 100%">
        
        <!-- 1. 基础组件 Basic -->
        <section id="section-basic">
          <el-card>
            <template #header>
              <span>基础组件 (Basic)</span>
            </template>
            <h3>Button 按钮</h3>
            <el-space wrap>
              <el-button>Default</el-button>
              <el-button type="primary">Primary</el-button>
              <el-button type="success">Success</el-button>
              <el-button type="info">Info</el-button>
              <el-button type="warning">Warning</el-button>
              <el-button type="danger">Danger</el-button>
            </el-space>
            <div style="margin-top: 10px;">
              <el-space wrap>
                <el-button plain>Plain</el-button>
                <el-button type="primary" plain>Primary</el-button>
                <el-button type="success" plain>Success</el-button>
                <el-button type="warning" plain>Warning</el-button>
                <el-button type="danger" plain>Danger</el-button>
              </el-space>
            </div>
            <div style="margin-top: 10px;">
              <el-space wrap>
                <el-button round>Round</el-button>
                <el-button type="primary" round>Primary</el-button>
                <el-button type="success" round>Success</el-button>
                <el-button type="info" round>Info</el-button>
                <el-button type="warning" round>Warning</el-button>
                <el-button type="danger" round>Danger</el-button>
              </el-space>
            </div>
            <div style="margin-top: 10px;">
               <el-button :icon="Search" circle />
               <el-button type="primary" :icon="Edit" circle />
               <el-button type="success" :icon="Check" circle />
               <el-button type="info" :icon="Message" circle />
               <el-button type="warning" :icon="Star" circle />
               <el-button type="danger" :icon="Delete" circle />
            </div>

            <el-divider />

            <h3>Link 链接</h3>
            <el-space wrap>
               <el-link href="#" target="_blank">Default</el-link>
               <el-link type="primary">Primary</el-link>
               <el-link type="success">Success</el-link>
               <el-link type="warning">Warning</el-link>
               <el-link type="danger">Danger</el-link>
               <el-link type="info">Info</el-link>
            </el-space>

            <el-divider />

            <h3>Icon 图标</h3>
            <el-space wrap style="font-size: 20px;">
              <el-icon><Edit /></el-icon>
              <el-icon><View /></el-icon>
              <el-icon><Share /></el-icon>
              <el-icon><Delete /></el-icon>
              <el-icon><Search /></el-icon>
              <el-icon class="is-loading"><Loading /></el-icon>
            </el-space>
          </el-card>
        </section>

        <!-- 2. 表单组件 Form -->
        <section id="section-form">
          <el-card>
            <template #header>
              <span>表单组件 (Form)</span>
            </template>
            <el-form :model="form" label-width="120px">
              <el-row :gutter="20">
                <el-col :span="12">
                  <el-form-item label="Input">
                    <el-input v-model="form.name" placeholder="Please input" />
                  </el-form-item>
                </el-col>
                <el-col :span="12">
                  <el-form-item label="Select">
                    <el-select v-model="form.region" placeholder="please select" style="width: 100%">
                      <el-option label="Option 1" value="1" />
                      <el-option label="Option 2" value="2" />
                    </el-select>
                  </el-form-item>
                </el-col>
              </el-row>

              <el-row :gutter="20">
                <el-col :span="12">
                  <el-form-item label="Date Picker">
                    <el-date-picker
                      v-model="form.date1"
                      type="date"
                      placeholder="Pick a date"
                      style="width: 100%"
                    />
                  </el-form-item>
                </el-col>
                <el-col :span="12">
                   <el-form-item label="Time Picker">
                    <el-time-picker v-model="form.date2" placeholder="Pick a time" style="width: 100%" />
                   </el-form-item>
                </el-col>
              </el-row>

              <el-form-item label="Switch">
                <el-switch v-model="form.delivery" />
              </el-form-item>

              <el-form-item label="Checkbox">
              <el-checkbox-group v-model="form.type">
                <el-checkbox label="勾选框" name="type" />
                <el-checkbox label="选中项目" name="type" />
              </el-checkbox-group>
            </el-form-item>

            <el-form-item label="Radio">
              <el-radio-group v-model="form.resource">
                <el-radio label="待勾选项目" />
                <el-radio label="选中项目" />
              </el-radio-group>
            </el-form-item>

              <el-form-item label="Slider">
                <el-slider v-model="form.slider" />
              </el-form-item>
              
              <el-form-item label="Rate">
                <el-rate v-model="form.rate" />
              </el-form-item>

               <el-form-item label="Input Number">
                <el-input-number v-model="form.num" :min="1" :max="10" />
              </el-form-item>

              <el-form-item>
                <el-button type="primary" @click="onSubmit">Create</el-button>
                <el-button>Cancel</el-button>
              </el-form-item>
            </el-form>
          </el-card>
        </section>

        <!-- 3. 数据展示 Data -->
        <section id="section-data">
          <el-card>
            <template #header>
              <span>数据展示 (Data)</span>
            </template>
            <h3>Table 表格</h3>
            <el-table :data="tableData" style="width: 100%; margin-bottom: 20px;" stripe border>
              <el-table-column prop="date" label="Date" width="150" />
              <el-table-column prop="name" label="Name" width="120" />
              <el-table-column prop="address" label="Address" />
              <el-table-column label="Status" width="100">
                <template #default="scope">
                  <el-tag :type="scope.row.tag === 'Home' ? '' : 'success'">{{ scope.row.tag }}</el-tag>
                </template>
              </el-table-column>
            </el-table>
            
            <div style="display: flex; justify-content: space-between; align-items: center;">
               <el-pagination background layout="prev, pager, next" :total="100" />
            </div>
            
            <el-divider />

            <h3>Tag 标签</h3>
            <el-space wrap>
              <el-tag>Tag 1</el-tag>
              <el-tag type="success">Tag 2</el-tag>
              <el-tag type="info">Tag 3</el-tag>
              <el-tag type="warning">Tag 4</el-tag>
              <el-tag type="danger">Tag 5</el-tag>
            </el-space>

            <el-divider />

            <h3>Progress 进度条</h3>
            <div style="width: 300px">
              <el-progress :percentage="50" />
              <el-progress :percentage="100" status="success" style="margin-top: 10px" />
              <el-progress :percentage="70" status="warning" style="margin-top: 10px" />
              <el-progress :percentage="50" status="exception" style="margin-top: 10px" />
            </div>

            <el-divider />
            
            <h3>Badge 徽章</h3>
            <el-space :size="30">
              <el-badge :value="12" class="item">
                <el-button>comments</el-button>
              </el-badge>
              <el-badge :value="3" class="item" type="primary">
                <el-button>replies</el-button>
              </el-badge>
               <el-badge :value="1" class="item" type="warning">
                <el-button>replies</el-button>
              </el-badge>
              <el-badge is-dot class="item">
                <el-button>query</el-button>
              </el-badge>
            </el-space>
            
            <el-divider />

            <h3>Avatar 头像</h3>
             <el-space :size="20">
               <el-avatar :size="50" :src="'https://cube.elemecdn.com/3/7c/3ea6beec64369c2642b92c6726f1epng.png'" />
               <el-avatar :size="50"> user </el-avatar>
             </el-space>
          </el-card>
        </section>

        <!-- 4. 导航 Navigation -->
        <section id="section-nav">
          <el-card>
            <template #header>
              <span>导航 (Navigation)</span>
            </template>
             <h3>Tabs 标签页</h3>
             <el-tabs v-model="activeTab" class="demo-tabs">
              <el-tab-pane label="User" name="first">User Config</el-tab-pane>
              <el-tab-pane label="Config" name="second">Config Manager</el-tab-pane>
              <el-tab-pane label="Role" name="third">Role Manager</el-tab-pane>
              <el-tab-pane label="Task" name="fourth">Task Manager</el-tab-pane>
            </el-tabs>

            <el-divider />

            <h3>Steps 步骤条</h3>
            <el-steps :active="1" align-center>
              <el-step title="Step 1" description="Some description" />
              <el-step title="Step 2" description="Some description" />
              <el-step title="Step 3" description="Some description" />
              <el-step title="Step 4" description="Some description" />
            </el-steps>

            <el-divider />

            <h3>Breadcrumb 面包屑</h3>
            <el-breadcrumb separator="/">
              <el-breadcrumb-item :to="{ path: '/' }">homepage</el-breadcrumb-item>
              <el-breadcrumb-item><a href="/">promotion management</a></el-breadcrumb-item>
              <el-breadcrumb-item>promotion list</el-breadcrumb-item>
              <el-breadcrumb-item>promotion detail</el-breadcrumb-item>
            </el-breadcrumb>
          </el-card>
        </section>

        <!-- 5. 反馈 Feedback -->
        <section id="section-feedback">
          <el-card>
            <template #header>
              <span>反馈 (Feedback)</span>
            </template>
            <h3>Alert 警告</h3>
            <div style="max-width: 600px">
              <el-alert title="Success alert" type="success" show-icon style="margin-bottom: 10px;" />
              <el-alert title="Info alert" type="info" show-icon style="margin-bottom: 10px;" />
              <el-alert title="Warning alert" type="warning" show-icon style="margin-bottom: 10px;" />
              <el-alert title="Error alert" type="error" show-icon />
            </div>

            <el-divider />

            <h3>Message / Notification / Dialog</h3>
            <el-space wrap>
              <el-button plain @click="openMessage">Open Message</el-button>
              <el-button plain @click="openNotification">Open Notification</el-button>
              <el-button plain @click="dialogVisible = true">Open Dialog</el-button>
              <el-button plain @click="drawer = true">Open Drawer</el-button>
            </el-space>

            <el-divider />
            
            <h3>Tooltip & Popover</h3>
             <el-space wrap>
              <el-tooltip content="Top Center prompts info" placement="top">
                <el-button>Tooltip</el-button>
              </el-tooltip>

              <el-popover
                placement="top-start"
                title="Title"
                :width="200"
                trigger="hover"
                content="this is content, this is content, this is content"
              >
                <template #reference>
                  <el-button>Popover</el-button>
                </template>
              </el-popover>
              
              <el-popconfirm title="Are you sure to delete this?">
                <template #reference>
                  <el-button>Popconfirm</el-button>
                </template>
              </el-popconfirm>
             </el-space>
            

            <el-dialog v-model="dialogVisible" title="Tips" width="30%">
              <span>This is a message</span>
              <template #footer>
                <span class="dialog-footer">
                  <el-button @click="dialogVisible = false">Cancel</el-button>
                  <el-button type="primary" @click="dialogVisible = false">Confirm</el-button>
                </span>
              </template>
            </el-dialog>

            <el-drawer v-model="drawer" title="I am the title" :with-header="false">
              <span>Hi there!</span>
            </el-drawer>
          </el-card>
        </section>

        <!-- 6. 其他 Others -->
        <section id="section-others">
          <el-card>
            <template #header>
              <span>其他 (Others)</span>
            </template>
            <h3>Collapse 折叠面板</h3>
            <el-collapse v-model="activeNames">
              <el-collapse-item title="Consistency" name="1">
                <div>Consistent with real life: in line with the process and logic of real life, and comply with languages and habits that the users are used to;</div>
              </el-collapse-item>
              <el-collapse-item title="Feedback" name="2">
                <div>Operation feedback: enable the users to clearly perceive their operations by style updates and interactive effects;</div>
              </el-collapse-item>
            </el-collapse>
            
            <el-divider />

            <h3>Skeleton 骨架屏</h3>
            <el-skeleton :rows="3" animated />
            
            <el-divider />
            
            <h3>Empty 空状态</h3>
            <el-empty description="description" :image-size="100" />
          </el-card>
        </section>
        
      </el-space>

      <!-- 7. 使用说明 Usage (独立页面) -->
      <div v-show="activePage === 'usage'" class="usage-page">
        <section id="section-usage">
          <el-card>
            <template #header>
              <span>使用说明 (Usage)</span>
            </template>
            <div style="line-height: 1.8; color: #606266;">
              <p>本主题基于 Element Plus 默认样式进行深度定制，实现了拟物化 (Skeuomorphism) 风格。</p>
              
              <div style="margin: 20px 0; padding: 30px; background-color: #FAFAFA; border: 1px dashed #DCDCDC; border-radius: 8px; text-align: center;">
                <p style="margin-top: 0; margin-bottom: 15px; color: #333; font-weight: 500;">获取样式配置文件</p>
                <el-button type="primary" size="large" :icon="CopyDocument" @click="copyConfig">
                  一键复制 index.scss 内容 (Copy Config)
                </el-button>
                <p style="margin-bottom: 0; margin-top: 10px; font-size: 12px; color: #999;">点击按钮即可将完整 SCSS 代码复制到剪贴板</p>
              </div>

              <h4 style="margin: 20px 0 10px; color: #303133;">引入方式</h4>
              <p>在项目的入口文件 (如 <code>main.ts</code> 或 <code>main.js</code>) 中引入样式文件即可生效：</p>
              
              <HoverCopyButton content="import './styles/element/index.scss'">
                <div style="background: #F5F7FA; padding: 15px; border-radius: 4px; margin: 10px 0; border: 1px solid #EBEEF5;">
                  <code style="font-family: Consolas, monospace; color: #409EFF;">
                    import './styles/element/index.scss'
                  </code>
                </div>
              </HoverCopyButton>

              <h4 style="margin: 20px 0 10px; color: #303133;">注意事项</h4>
              <ul style="padding-left: 20px; list-style-type: disc;">
                <li>请确保在引入 Element Plus 默认样式之后引入本样式文件，以保证覆盖生效。</li>
                <li>本样式文件使用了 SCSS 编写，请确保项目已配置 SCSS 预处理器。</li>
                <li>样式主要针对常用组件进行了定制，如需更多组件支持，请在 <code>src/styles/element/index.scss</code> 中继续添加。</li>
              </ul>
            </div>
          </el-card>
        </section>
      </div>
    </main>
    </div>
  </div>
</template>

<script setup lang="ts">
import { reactive, ref, onMounted, nextTick } from 'vue'
import { ElMessage, ElNotification } from 'element-plus'
import 'element-plus/theme-chalk/src/message.scss'
import 'element-plus/theme-chalk/src/notification.scss'
import {
  Search,
  Edit,
  Check,
  Message,
  Star,
  Delete,
  View,
  Share,
  Loading,
  CopyDocument
} from '@element-plus/icons-vue'
import HoverCopyButton from '@/components/HoverCopyButton.vue'

// Import SCSS content
import indexScssContent from '@/styles/element/index.scss?raw'

const copyConfig = async () => {
  try {
    await navigator.clipboard.writeText(indexScssContent)
    ElMessage.success('复制成功')
  } catch (err) {
    ElMessage.error('复制失败，请手动复制')
    console.error('Failed to copy text: ', err)
  }
}

// Sidebar Menu Items
const menuItems = [
  { id: 'section-basic', title: '基础组件' },
  { id: 'section-form', title: '表单组件' },
  { id: 'section-data', title: '数据展示' },
  { id: 'section-nav', title: '导航' },
  { id: 'section-feedback', title: '反馈' },
  { id: 'section-others', title: '其他' },
]

const activeSection = ref('section-basic')
const activePage = ref('demo') // 'demo' | 'usage'
const activeTopMenu = ref('components') // 'home' | 'components'

const handleTopMenuSelect = (key: string) => {
  activeTopMenu.value = key
  if (key === 'home') {
    // 首页 -> 使用说明
    activePage.value = 'usage'
    activeSection.value = '' // 清空侧边栏选中
    window.scrollTo({ top: 0, behavior: 'smooth' })
  } else if (key === 'components') {
    // 组件 -> 演示页面 (默认基础组件)
    activePage.value = 'demo'
    activeSection.value = 'section-basic'
    nextTick(() => {
      scrollToSection('section-basic')
    })
  }
}

const scrollToSection = (id: string) => {
  activeSection.value = id
  
  // 仅在演示模式下处理滚动
  if (activePage.value === 'demo') {
    // 等待 DOM 更新，因为 v-show 切换可能需要时间
    nextTick(() => {
      const element = document.getElementById(id)
      if (element) {
        // 平滑滚动，并预留一点顶部距离
        const offset = 80 // 增加偏移量以避开顶部 Header
        const bodyRect = document.body.getBoundingClientRect().top
        const elementRect = element.getBoundingClientRect().top
        const elementPosition = elementRect - bodyRect
        const offsetPosition = elementPosition - offset

        window.scrollTo({
          top: offsetPosition,
          behavior: 'smooth'
        })
      }
    })
  }
}

// 监听滚动以高亮侧边栏
onMounted(() => {
  window.addEventListener('scroll', () => {
    let current = ''
    menuItems.forEach(item => {
      const section = document.getElementById(item.id)
      if (section) {
        const sectionTop = section.offsetTop
        if (window.scrollY >= sectionTop - 100) {
          current = item.id
        }
      }
    })
    if (current && activePage.value === 'demo') {
      activeSection.value = current
    }
  })
})


// Form Data
const form = reactive({
  name: '',
  region: '',
  date1: '',
  date2: '',
  delivery: false,
  type: ['选中项目'], // 默认选中 '选中项目'
  resource: '选中项目', // 默认选中 '选中项目'
  desc: '',
  slider: 50,
  rate: 3.5,
  num: 1
})

const onSubmit = () => {
  console.log('submit!')
}

// Table Data
const tableData = [
  {
    date: '2016-05-03',
    name: 'Tom',
    address: 'No. 189, Grove St, Los Angeles',
    tag: 'Home',
  },
  {
    date: '2016-05-02',
    name: 'Tom',
    address: 'No. 189, Grove St, Los Angeles',
    tag: 'Office',
  },
  {
    date: '2016-05-04',
    name: 'Tom',
    address: 'No. 189, Grove St, Los Angeles',
    tag: 'Home',
  },
]

// Tabs
const activeTab = ref('first')

// Dialog & Drawer
const dialogVisible = ref(false)
const drawer = ref(false)

// Collapse
const activeNames = ref(['1'])

// Message & Notification
const openMessage = () => {
  ElMessage.success('This is a success message')
}
const openNotification = () => {
  ElNotification({
    title: 'Success',
    message: 'This is a success message',
    type: 'success',
  })
}
</script>

<style scoped lang="scss">
.app-container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.top-header {
  position: sticky;
  top: 0;
  z-index: 1000;
  background: #fff;
  border-bottom: 1px solid #dcdcdc;
  box-shadow: 0 2px 4px rgba(0,0,0,0.05);

  .header-content {
    max-width: 1200px;
    margin: 0 auto;
    display: flex;
    align-items: center;
    padding: 0 20px;
    height: 60px;
  }

  .logo {
    font-size: 18px;
    font-weight: 600;
    color: #333;
    margin-right: 40px;
    // 拟物化文字效果
    text-shadow: 0 1px 0 #fff;
    
    .logo-subtitle {
      font-size: 12px;
      font-weight: normal;
      color: #999;
      margin-left: 8px;
      vertical-align: middle;
    }
  }

  .top-menu {
    border-bottom: none;
    background: transparent;
    flex: 1;
    
    :deep(.el-menu-item) {
      font-size: 16px;
      font-weight: 500;
      color: #666;
      
      &:hover {
        background-color: transparent;
        color: var(--el-color-primary);
      }
      
      &.is-active {
        color: var(--el-color-primary);
        border-bottom-width: 3px;
      }
    }
  }
  
  .menu-extra {
    display: flex;
    align-items: center;
    gap: 15px;
  }
  
  .external-link {
    color: #666;
    text-decoration: none;
    font-size: 14px;
    padding: 8px 12px;
    border-radius: 4px;
    transition: all 0.3s;
    white-space: nowrap;
    
    &:hover {
      color: var(--el-color-primary);
      background-color: #f5f7fa;
    }
  }
  
  .version-info {
    color: #999;
    font-size: 14px;
  }
}

.components-demo-layout {
  display: flex;
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  gap: 20px;
  flex: 1; // 占满剩余空间
  width: 100%; // 确保宽度
}

// 侧边栏样式
.sidebar {
  width: 200px;
  flex-shrink: 0;
  
  // 固定定位逻辑 (配合 sticky header)
  position: sticky;
  top: 80px; // Header height (60) + padding (20)
  height: fit-content;
  
  .sidebar-menu {
    background: #FFFFFF;
    border-radius: 8px;
    box-shadow: 0 1px 2px rgba(0,0,0,0.05);
    border: 1px solid #DCDCDC;
    padding: 10px 0;
    overflow: hidden;
  }
  
  .menu-item {
    padding: 12px 20px;
    cursor: pointer;
    font-size: 14px;
    color: #666666;
    transition: all 0.2s;
    border-left: 3px solid transparent;
    
    &:hover {
      background-color: #F5F5F5;
      color: #333333;
    }
    
    &.active {
      background-color: #FAFAFA;
      color: var(--el-color-primary);
      border-left-color: var(--el-color-primary);
      font-weight: 500;
    }
  }
}

.usage-page {
    width: 100%;
    
    // 确保使用说明页面的卡片也能撑开
    #section-usage {
      width: 100%;
    }
  }

  .main-content {
    flex: 1;
    min-width: 0; // 防止 flex 子项溢出
  }

h3 {
  margin: 15px 0 10px;
  color: var(--el-text-color-regular);
  font-size: 16px;
  font-weight: 500;
}
/* .el-card {
  margin-bottom: 20px;
} */
</style>
