<template>
   <div class="app-container">
    <el-table
        :data="tableListData"
        style="width: 100%">
        <el-table-column 
        type="index"
        width="50">
        </el-table-column>
        <el-table-column
            prop="date"
            width="150"
            label="日期">
        </el-table-column>
        <el-table-column
            prop="describe"
            label="描述">
        </el-table-column>
        <el-table-column
            prop="order"
            label="执行命令"
           >
        </el-table-column>
        <el-table-column
            prop="img"
            width="260"
            label="img"
           >
            <template scope="scope">
              <el-image 
                  style="width: 35px; height: 35px"
                  :src="scope.row.img" 
                  :preview-src-list="imgSrcList(scope.row.img)">
              </el-image>
            </template>
        </el-table-column>
           <el-table-column
            prop="detailDescribe"
            label="详细描述">
        </el-table-column>
         <el-table-column
            fixed="right"
            label="操作"
            width="100">
            <template slot-scope="scope">
                <el-button @click="handleClick(scope.row)" type="text" size="small">查看</el-button>
            </template>
        </el-table-column>
    </el-table>
     <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="initCurrentPage"
      :page-sizes="[10, 20, 30, 40]"
      :page-size="pageSize"
      layout="total, sizes, prev, pager, next, jumper"
      :total="total">
    </el-pagination>
   </div>
</template>
 <script>
    export default {
      data() {
        return {
          numberPage:10,//每页条数
          initCurrentPage: 1, //默认当前页为1
          currentPage:1,
          total:0, //总共多少条数据
          pageSize:1, //当前第几页
          tableListData:[],
          tableData: [{
            date: '2021-09-29',
            order: 'git config --global user.name "xxx" / git config --global user.email "xxxxx.com"',
            img:require('@/assets/images/git/git5.png'),
            describe: '创建自己的git用户',
            detailDescribe:'',
          }, {
            date: '2021-09-29',
            order: 'git config  --list',
            img:require('@/assets/images/git/git6.png'),
            describe: '查看git中的配置列表',
             detailDescribe:'',
          }, {
            date: '2021-09-29',
            order: 'git clone [url]',
            img:require('@/assets/images/git/git7.png'),
            describe: '拷贝一个 Git 仓库到本地',
             detailDescribe:'',
          }, {
            date: '2021-09-30',
            order: 'git branch <name>',
            img:require('@/assets/images/git/git8.png'),
            describe: '创建分支',
             detailDescribe:'',
          }, {
            date: '2021-09-30',
            order: 'git branch -a / git branch',
            img:require('@/assets/images/git/git9.png'),
            describe: '查看所有分支与查看当前使用分支',
             detailDescribe:'',
          }, {
            date: '2021-09-30',
            order: 'git checkout [分支名]',
            img:require('@/assets/images/git/git10.png'),
            describe: '切换分支',
             detailDescribe:'',
          }, {
            date: '2021-09-30',
            order: 'git status / git status -s',
            img:require('@/assets/images/git/git11.png'),
            describe: '查看工作区状态',
             detailDescribe:'',
          }, {
            date: '2021-09-30',
            order: 'git add .',
            img:require('@/assets/images/git/git12.png'),
            describe: '全部添加到缓存区',
             detailDescribe:'',
          },{
            date: '2021-09-30',
            order: 'git commit -m "提交代码说明"',
            img:require('@/assets/images/git/git14.png'),
            describe: '暂存区内容添加到本地仓库中',
             detailDescribe:'',
          },
          {
            date: '2021-09-30',
            order: 'git pull origin main',
            img:require('@/assets/images/git/git13.png'),
            describe: '拉取代码',
             detailDescribe:'',
          },{
            date: '2021-09-29',
            order: 'git push origin 分支名:主分支名',
            img:require('@/assets/images/git/git15.png'),
            describe: '分支向主分支提交代码',
             detailDescribe:'',
          },{
            date: '2021-09-29',
            order: '',
            img:require('@/assets/images/git/git16.png'),
            describe: '解决冲突',
             detailDescribe:'先找到冲突文件，解决完冲突文件之后,重新添加，提交，然后再次进行推与拉',
          },{
            date: '2021-09-29',
            order: 'git ls-files',
            img:require('@/assets/images/git/git17.png'),
            describe: '查看暂存区中文件信息',
            detailDescribe:"",
          }, {
            date: '2021-09-29',
            order: 'git log',
            img:require('@/assets/images/git/git3.png'),
            describe: '查看git（git log）提交历次记录',
            detailDescribe:'可以显示所有提交过的版本信息，不包括已经被删除的 commit 记录和 reset 的操作'
          }, {
            date: '2021-09-29',
            order: 'git reset --hard "commit id"',
            img:require('@/assets/images/git/git4.png'),
            describe: '回退git log指定的commit id',
            detailDescribe:'回退git log指定的commit id,commit id要加单引号',
          }, {
            date: '2021-09-29',
            order: 'git reflog',
            img:require('@/assets/images/git/git7.png'),
            describe: '查看git（git reflog）提交历次记录',
            detailDescribe:'是显示所有的操作记录，包括提交，回退的操作。一般用来找出操作记录中的版本号，进行回退,git reflog常用于恢复本地的错误操作',
          },{
            date: '2021-09-29',
            order: 'git reset --hard 版本号',
            img:require('@/assets/images/git/git4.png'),
            describe: '回退git reflog',
            detailDescribe:'回退git reflog前面的版本号,版本号不加单引号',
          }]
        }
      },
      mounted(){
        this.tableListData=this.tableData.slice(0,10);
        this.total=this.tableData.length;
      },
      methods:{
        // 加载图片放大
          imgSrcList(imgUrl){
            const imgurls=[];
            imgurls.push(imgUrl);
            return imgurls
          },
          // 翻页方法
          handleSizeChange(val) {
            this.numberPage=val; //改变每页显示条数
            this.tableListData=this.tableData.slice(1,val);
          //  console.log(`每页 ${val} 条`);
          },
           handleCurrentChange(val) {
              this.currentPage=val-1;
              // 从表格数据截取,从当前页数减1开始*每页显示的条数numberPage，截取到当前页*当前显示的位置
              // 例 第1页 this.tableData.slice(0*10,1*10) 从下标0处开始，截取到下标为10的数据
              //    第2页 this.tableData.slice(1*10,2*10) 从下标11处开始，截取到下标为20的数据
               console.log(this.tableData.slice(10))
               console.log(this.tableData.slice(0,10))
              this.tableListData=this.tableData.slice(this.currentPage*this.numberPage,val*this.numberPage);
              //console.log(`当前页: ${val}`);
          }
      },
    }
  </script>-