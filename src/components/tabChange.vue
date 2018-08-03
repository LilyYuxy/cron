<template>
<el-row class="tab-container">
    <el-row class="contents">
    <el-row class="title" :gutter="1">
      <el-col :span="1">&nbsp;</el-col>
      <el-col :span="3" v-for="(item, index) in list" :key="index" @click.native="change(index)" :class="{'active': showIndex == index}">
        <div>{{item.name}}</div>
      </el-col>
    </el-row>
    <el-row class="main">
      <!-- 秒 -->
      <el-row v-if="showIndex == 0" class="minutes">
        <el-row>
          <el-col :span="1">
            <el-radio :label="0" v-model="seconds" @change="changeRadio"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>每秒 允许的通配符[, - * /]</span>
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="1" v-model="seconds" @change="changeRadio"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>周期从</span>
            <el-input type="number" :disabled="seconds !== 1" :max="59" :min="1" class="nums" v-model.number="startSec" @click.native="submit"></el-input>-
            <el-input type="number" :disabled="seconds !== 1" :max="59" :min="2" class="nums" v-model.number="endSec" @click.native="submit"></el-input>秒
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="2" v-model="seconds" @change="changeRadio"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>从</span>
            <el-input type="number" :disabled="seconds !== 2" :max="59" :min="0" class="nums" v-model.number="startSecond" @click.native="submit"></el-input>秒开始，每
            <el-input type="number" :disabled="seconds !== 2" :max="59" :min="1" class="nums" v-model.number="intervalTime" @click.native="submit"></el-input>秒执行一次
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="3" v-model="seconds" @change="changeRadio"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>指定秒</span>
            <el-checkbox-group v-model="checkSecond" @change="checkSeconds" @click.native="submit">
              <el-row>
                <el-checkbox label="00"></el-checkbox>
                <el-checkbox label="01"></el-checkbox>
                <el-checkbox label="02"></el-checkbox>
                <el-checkbox label="03"></el-checkbox>
                <el-checkbox label="04"></el-checkbox>
                <el-checkbox label="05"></el-checkbox>
                <el-checkbox label="06"></el-checkbox>
                <el-checkbox label="07"></el-checkbox>
                <el-checkbox label="08"></el-checkbox>
                <el-checkbox label="09"></el-checkbox>
              </el-row>
              <el-row>
                <el-checkbox label="10"></el-checkbox>
                <el-checkbox label="11"></el-checkbox>
                <el-checkbox label="12"></el-checkbox>
                <el-checkbox label="13"></el-checkbox>
                <el-checkbox label="14"></el-checkbox>
                <el-checkbox label="15"></el-checkbox>
                <el-checkbox label="16"></el-checkbox>
                <el-checkbox label="17"></el-checkbox>
                <el-checkbox label="18"></el-checkbox>
                <el-checkbox label="19"></el-checkbox>
              </el-row>
              <el-row>
                <el-checkbox label="20"></el-checkbox>
                <el-checkbox label="21"></el-checkbox>
                <el-checkbox label="22"></el-checkbox>
                <el-checkbox label="23"></el-checkbox>
                <el-checkbox label="24"></el-checkbox>
                <el-checkbox label="25"></el-checkbox>
                <el-checkbox label="26"></el-checkbox>
                <el-checkbox label="27"></el-checkbox>
                <el-checkbox label="28"></el-checkbox>
                <el-checkbox label="29"></el-checkbox>
              </el-row>
              <el-row>
                <el-checkbox label="30"></el-checkbox>
                <el-checkbox label="31"></el-checkbox>
                <el-checkbox label="32"></el-checkbox>
                <el-checkbox label="33"></el-checkbox>
                <el-checkbox label="34"></el-checkbox>
                <el-checkbox label="35"></el-checkbox>
                <el-checkbox label="36"></el-checkbox>
                <el-checkbox label="37"></el-checkbox>
                <el-checkbox label="38"></el-checkbox>
                <el-checkbox label="39"></el-checkbox>
              </el-row>
              <el-row>
                <el-checkbox label="40"></el-checkbox>
                <el-checkbox label="41"></el-checkbox>
                <el-checkbox label="42"></el-checkbox>
                <el-checkbox label="43"></el-checkbox>
                <el-checkbox label="44"></el-checkbox>
                <el-checkbox label="45"></el-checkbox>
                <el-checkbox label="46"></el-checkbox>
                <el-checkbox label="47"></el-checkbox>
                <el-checkbox label="48"></el-checkbox>
                <el-checkbox label="49"></el-checkbox>
              </el-row>
              <el-row>
                <el-checkbox label="50"></el-checkbox>
                <el-checkbox label="51"></el-checkbox>
                <el-checkbox label="52"></el-checkbox>
                <el-checkbox label="53"></el-checkbox>
                <el-checkbox label="54"></el-checkbox>
                <el-checkbox label="55"></el-checkbox>
                <el-checkbox label="56"></el-checkbox>
                <el-checkbox label="57"></el-checkbox>
                <el-checkbox label="58"></el-checkbox>
                <el-checkbox label="59"></el-checkbox>
              </el-row>
              
            </el-checkbox-group>

          </el-col>
        </el-row>

      </el-row>

      <!-- 分 -->
      <el-row v-if="showIndex == 1" class="minutes">
        <el-row>
          <el-col :span="1">
            <el-radio :label="0" v-model="minutes" @change="changeRadioMinute"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>每分 允许的通配符[, - * /]</span>
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="1" v-model="minutes" @change="changeRadioMinute"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>周期从</span>
            <el-input type="number" :disabled="minutes !== 1" :max="59" :min="1" class="nums" v-model.number="startMin" @click.native="submit"></el-input>-
            <el-input type="number" :disabled="minutes !== 1" :max="59" :min="2" class="nums" v-model.number="endMin" @click.native="submit"></el-input>分  
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="2" v-model="minutes" @change="changeRadioMinute"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>从</span>
            <el-input type="number" :disabled="minutes !== 2" :max="59" :min="0" class="nums" v-model.number="startMinute" @click.native="submit"></el-input>分开始，每
            <el-input type="number" :disabled="minutes !== 2" :max="59" :min="1" class="nums" v-model.number="intervalMinute" @click.native="submit"></el-input>分钟执行一次
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="3" v-model="minutes" @change="changeRadioMinute"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>指定分钟</span>
            <el-checkbox-group v-model="checkMinute" @change="checkMinutes" @click.native="submit">
              <el-row>
                <el-checkbox label="00"></el-checkbox>
                <el-checkbox label="01"></el-checkbox>
                <el-checkbox label="02"></el-checkbox>
                <el-checkbox label="03"></el-checkbox>
                <el-checkbox label="04"></el-checkbox>
                <el-checkbox label="05"></el-checkbox>
                <el-checkbox label="06"></el-checkbox>
                <el-checkbox label="07"></el-checkbox>
                <el-checkbox label="08"></el-checkbox>
                <el-checkbox label="09"></el-checkbox>
              </el-row>
              <el-row>
                <el-checkbox label="10"></el-checkbox>
                <el-checkbox label="11"></el-checkbox>
                <el-checkbox label="12"></el-checkbox>
                <el-checkbox label="13"></el-checkbox>
                <el-checkbox label="14"></el-checkbox>
                <el-checkbox label="15"></el-checkbox>
                <el-checkbox label="16"></el-checkbox>
                <el-checkbox label="17"></el-checkbox>
                <el-checkbox label="18"></el-checkbox>
                <el-checkbox label="19"></el-checkbox>
              </el-row>
              <el-row>
                <el-checkbox label="20"></el-checkbox>
                <el-checkbox label="21"></el-checkbox>
                <el-checkbox label="22"></el-checkbox>
                <el-checkbox label="23"></el-checkbox>
                <el-checkbox label="24"></el-checkbox>
                <el-checkbox label="25"></el-checkbox>
                <el-checkbox label="26"></el-checkbox>
                <el-checkbox label="27"></el-checkbox>
                <el-checkbox label="28"></el-checkbox>
                <el-checkbox label="29"></el-checkbox>
              </el-row>
              <el-row>
                <el-checkbox label="30"></el-checkbox>
                <el-checkbox label="31"></el-checkbox>
                <el-checkbox label="32"></el-checkbox>
                <el-checkbox label="33"></el-checkbox>
                <el-checkbox label="34"></el-checkbox>
                <el-checkbox label="35"></el-checkbox>
                <el-checkbox label="36"></el-checkbox>
                <el-checkbox label="37"></el-checkbox>
                <el-checkbox label="38"></el-checkbox>
                <el-checkbox label="39"></el-checkbox>
              </el-row>
              <el-row>
                <el-checkbox label="40"></el-checkbox>
                <el-checkbox label="41"></el-checkbox>
                <el-checkbox label="42"></el-checkbox>
                <el-checkbox label="43"></el-checkbox>
                <el-checkbox label="44"></el-checkbox>
                <el-checkbox label="45"></el-checkbox>
                <el-checkbox label="46"></el-checkbox>
                <el-checkbox label="47"></el-checkbox>
                <el-checkbox label="48"></el-checkbox>
                <el-checkbox label="49"></el-checkbox>
              </el-row>
              <el-row>
                <el-checkbox label="50"></el-checkbox>
                <el-checkbox label="51"></el-checkbox>
                <el-checkbox label="52"></el-checkbox>
                <el-checkbox label="53"></el-checkbox>
                <el-checkbox label="54"></el-checkbox>
                <el-checkbox label="55"></el-checkbox>
                <el-checkbox label="56"></el-checkbox>
                <el-checkbox label="57"></el-checkbox>
                <el-checkbox label="58"></el-checkbox>
                <el-checkbox label="59"></el-checkbox>
              </el-row>
              
            </el-checkbox-group>

          </el-col>
        </el-row>
      </el-row>

      <!-- 时 -->
      <el-row v-if="showIndex == 2" class="minutes">
        <el-row>
          <el-col :span="1">
            <el-radio :label="0" v-model="hours" @change="changeRadioHour"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>每小时 允许的通配符[, - * /]</span>
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="1" v-model="hours" @change="changeRadioHour"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>周期从</span>
            <el-input type="number" :disabled="hours !== 1" :max="23" :min="0" class="nums" v-model.number="startHou" @click.native="submit"></el-input>-
            <el-input type="number" :disabled="hours !== 1" :max="23" :min="1 " class="nums" v-model.number="endHour" @click.native="submit"></el-input>小时  
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="2" v-model="hours" @change="changeRadioHour"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>从</span>
            <el-input type="number" :disabled="hours !== 2" :max="23" :min="0" class="nums" v-model.number="startHour" @click.native="submit"></el-input>时开始，每
            <el-input type="number" :disabled="hours !== 2" :max="23" :min="1" class="nums" v-model.number="intervalHour" @click.native="submit"></el-input>小时执行一次
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="3" v-model="hours" @change="changeRadioHour"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>指定</span>
            <el-checkbox-group v-model="checkHour" @change="checkHours" @click.native="submit">
              <el-row>
                <el-checkbox label="00"></el-checkbox>
                <el-checkbox label="01"></el-checkbox>
                <el-checkbox label="02"></el-checkbox>
                <el-checkbox label="03"></el-checkbox>
                <el-checkbox label="04"></el-checkbox>
                <el-checkbox label="05"></el-checkbox>
                <el-checkbox label="06"></el-checkbox>
                <el-checkbox label="07"></el-checkbox>
                <el-checkbox label="08"></el-checkbox>
                <el-checkbox label="09"></el-checkbox>
                <el-checkbox label="10"></el-checkbox>
                <el-checkbox label="11"></el-checkbox>
              </el-row>
              <el-row>
                <el-checkbox label="12"></el-checkbox>
                <el-checkbox label="13"></el-checkbox>
                <el-checkbox label="14"></el-checkbox>
                <el-checkbox label="15"></el-checkbox>
                <el-checkbox label="16"></el-checkbox>
                <el-checkbox label="17"></el-checkbox>
                <el-checkbox label="18"></el-checkbox>
                <el-checkbox label="19"></el-checkbox>
                <el-checkbox label="20"></el-checkbox>
                <el-checkbox label="21"></el-checkbox>
                <el-checkbox label="22"></el-checkbox>
                <el-checkbox label="23"></el-checkbox>
              </el-row>
              
            </el-checkbox-group>
          </el-col>
        </el-row>
      </el-row>

      <!-- 日 -->
      <el-row v-if="showIndex == 3" class="minutes">
        <el-row>
          <el-col :span="1">
            <el-radio :label="0" v-model="days" @change="changeRadioDay"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>日 允许的通配符[, - * / L W]</span>
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="1" v-model="days" @change="changeRadioDay"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>不指定</span>
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="2" v-model="days" @change="changeRadioDay"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>周期从</span>
            <el-input type="number" :disabled="days !== 2" :max="31" :min="1" class="nums" v-model.number="startDay" @click.native="submit"></el-input>-
            <el-input type="number" :disabled="days !== 2" :max="31" :min="2" class="nums" v-model.number="endDay" @click.native="submit"></el-input>日  
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="3" v-model="days" @change="changeRadioDay"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>从</span>
            <el-input type="number" :disabled="days !== 3" :max="31" :min="1" class="nums" v-model.number="startDays" @click.native="submit"></el-input>日开始，每
            <el-input type="number" :disabled="days !== 3" :max="31" :min="1" class="nums" v-model.number="intervalDay" @click.native="submit"></el-input>日执行一次
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="4" v-model="days" @change="changeRadioDay"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>每月</span>
            <el-input type="number" :disabled="days !== 4" :max="31" :min="1" class="nums" v-model.number="workDay" @click.native="submit"></el-input>日最近的工作日
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="5" v-model="days" @change="changeRadioDay"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>每月最后一天</span>
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="6" v-model="days" @change="changeRadioDay"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>指定</span>
            <el-checkbox-group v-model="checkDay" @change="checkDays" @click.native="submit">
              <el-row>
                <el-checkbox label="1"></el-checkbox>
                <el-checkbox label="2"></el-checkbox>
                <el-checkbox label="3"></el-checkbox>
                <el-checkbox label="4"></el-checkbox>
                <el-checkbox label="5"></el-checkbox>
                <el-checkbox label="6"></el-checkbox>
                <el-checkbox label="7"></el-checkbox>
                <el-checkbox label="8"></el-checkbox>
                <el-checkbox label="9"></el-checkbox>
                <el-checkbox label="10"></el-checkbox>
                <el-checkbox label="11"></el-checkbox>
                <el-checkbox label="12"></el-checkbox>
                <el-checkbox label="13"></el-checkbox>
                <el-checkbox label="14"></el-checkbox>
                <el-checkbox label="15"></el-checkbox>
                <el-checkbox label="16"></el-checkbox>
              </el-row>
              <el-row>
                <el-checkbox label="17"></el-checkbox>
                <el-checkbox label="18"></el-checkbox>
                <el-checkbox label="19"></el-checkbox>
                <el-checkbox label="20"></el-checkbox>
                <el-checkbox label="21"></el-checkbox>
                <el-checkbox label="22"></el-checkbox>
                <el-checkbox label="23"></el-checkbox>
                <el-checkbox label="24"></el-checkbox>
                <el-checkbox label="25"></el-checkbox>
                <el-checkbox label="26"></el-checkbox>
                <el-checkbox label="27"></el-checkbox>
                <el-checkbox label="28"></el-checkbox>
                <el-checkbox label="29"></el-checkbox>
                <el-checkbox label="30"></el-checkbox>
                <el-checkbox label="31"></el-checkbox>
              </el-row>
              
            </el-checkbox-group>

          </el-col>
        </el-row>
      </el-row>

      <!-- 月 -->
      <el-row v-if="showIndex == 4" class="minutes">
        <el-row>
          <el-col :span="1">
            <el-radio :label="0" v-model="months" @change="changeRadioMonth"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>月 允许的通配符[, - * /]</span>
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="1" v-model="months" @change="changeRadioMonth"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>不指定</span>
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="2" v-model="months" @change="changeRadioMonth"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>周期从</span>
            <el-input type="number" :disabled="months !== 1" :max="59" :min="1" class="nums" v-model.number="startMon" @click.native="submit"></el-input>-
            <el-input type="number" :disabled="months !== 1" :max="59" :min="2" class="nums" v-model.number="endMon" @click.native="submit"></el-input>月 
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="3" v-model="months" @change="changeRadioMonth"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>从</span>
            <el-input type="number" :disabled="months !== 2" :max="59" :min="0" class="nums" v-model.number="startMonth" @click.native="submit"></el-input>日开始，每
            <el-input type="number" :disabled="months !== 2" :max="59" :min="1" class="nums" v-model.number="intervalMonth" @click.native="submit"></el-input>月执行一次
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="4" v-model="months" @change="changeRadioMonth"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>指定</span>
            <el-checkbox-group v-model="checkMonth" @change="checkMonths" @click.native="submit">
              <el-row>
                <el-checkbox label="1"></el-checkbox>
                <el-checkbox label="2"></el-checkbox>
                <el-checkbox label="3"></el-checkbox>
                <el-checkbox label="4"></el-checkbox>
                <el-checkbox label="5"></el-checkbox>
                <el-checkbox label="6"></el-checkbox>
                <el-checkbox label="7"></el-checkbox>
                <el-checkbox label="8"></el-checkbox>
                <el-checkbox label="9"></el-checkbox>
                <el-checkbox label="10"></el-checkbox>
                <el-checkbox label="11"></el-checkbox>
                <el-checkbox label="12"></el-checkbox>
              </el-row>
              
            </el-checkbox-group>

          </el-col>
        </el-row>
      </el-row>

      <!-- 周 -->
      <el-row v-if="showIndex == 5" class="minutes">
        <el-row>
          <el-col :span="1">
            <el-radio :label="0" v-model="weeks" @change="changeRadioWeek"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>不指定</span>
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="1" v-model="weeks" @change="changeRadioWeek"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>周 允许的通配符[, - * / L #]</span>
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="2" v-model="weeks" @change="changeRadioWeek"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>周期从星期</span>
            <el-input type="number" :max="7" :min="1" class="nums" v-model.number="startWeek" @click.native="submit"></el-input>-
            <el-input type="number" :max="7" :min="2" class="nums" v-model.number="endWeek" @click.native="submit"></el-input> 
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="3" v-model="weeks" @change="changeRadioWeek"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>第</span>
            <el-input type="number" :max="4" :min="1" class="nums" v-model.number="startWeeks" @click.native="submit"></el-input>周的星期
            <el-input type="number" :max="7" :min="1" class="nums" v-model.number="intervalWeek" @click.native="submit"></el-input>执行一次
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="4" v-model="weeks" @change="changeRadioWeek"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>本月最后一个星期</span>
            <el-input type="number" :max="7" :min="1" class="nums" v-model.number="lastWeek" @click.native="submit"></el-input>执行一次
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="5" v-model="weeks" @change="changeRadioWeek"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>指定</span>
            <el-checkbox-group v-model="checkWeek" @change="checkWeeks" @click.native="submit">
              <el-row>
                <el-checkbox label="1"></el-checkbox>
                <el-checkbox label="2"></el-checkbox>
                <el-checkbox label="3"></el-checkbox>
                <el-checkbox label="4"></el-checkbox>
                <el-checkbox label="5"></el-checkbox>
                <el-checkbox label="6"></el-checkbox>
                <el-checkbox label="7"></el-checkbox>
              </el-row>

            </el-checkbox-group>
            <span>(1表示星期天，2表示星期一， 依次类推)</span>

          </el-col>
        </el-row>
      </el-row>

      <!-- 年 -->
      <el-row v-if="showIndex == 6" class="minutes">
        <el-row>
          <el-col :span="1">
            <el-radio :label="0" v-model="years" @change="changeRadioYear"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>不指定 允许的通配符[, - * /]非必填</span>
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="1" v-model="years" @change="changeRadioYear"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>每年</span>
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="1">
            <el-radio :label="2" v-model="years" @change="changeRadioYear"></el-radio>
          </el-col>
          <el-col :span="16">
            <span>周期从</span>
            <el-input type="number" :disabled="years !== 2" :max="3000" :min="currentYear" class="nums" v-model.number="startYear"></el-input>-
            <el-input type="number" :disabled="years !== 2" :max="3000" :min="currentYear" class="nums" v-model.number="endYear"></el-input> 
          </el-col>
        </el-row>

      </el-row>

    </el-row>
    <el-row class="footer">
      <el-button type="primary" size="small" @click="submit()">确认</el-button>
      <el-button type="primary" size="small" @click="reset()">重置</el-button>
    </el-row>

    <el-row class="text">
      cron表达式为:&nbsp;&nbsp;<span>{{cronParams}}</span>
    </el-row>
  </el-row>
</el-row>

</template>

<script>
export  default {
  data () {
    return {
      cronParams: '',
      // tab切换数据
      list: [
        {name: '秒', index: 0},
        {name: '分', index: 1},
        {name: '时', index: 2},
        {name: '日', index: 3},
        {name: '月', index: 4},
        {name: '周', index: 5},
        {name: '年', index: 6},
      ],
      showIndex: 0, // 显示的索引

      seconds: 0, // 选择秒
      secondVal: '', // 提交秒
      startSec: 1, // 周期开始秒
      endSec: 2, // 周期结束秒
      startSecond: 0, // 开始秒
      intervalTime: 1, // 间隔秒
      checkSecond: [], // 指定秒数据

      minutes: 0, // 选择分钟
      minuteVal: '', // 提交分钟
      startMin: 1, // 周期开始分钟
      endMin: 2, // 周期结束分钟
      startMinute: 0, // 开始分钟
      intervalMinute: 1, // 间隔分钟
      checkMinute: [], // 指定分数据

      hours: 0, // 选择时
      hourVal: '', // 提交时
      startHou: 0, // 周期开始时
      endHour: 1, // 周期结束时
      startHour: 0, // 开始时
      intervalHour: 1, // 间隔时
      checkHour: [], // 指定时

      days: 0, // 选择天
      dayVal: '', // 提交天
      startDay: 1, // 周期开始天
      endDay: 2, // 周期结束天
      startDays: 1, // 开始天
      intervalDay: 1, // 间隔天
      checkDay: [], // 指定天
      workDay: 1, // 最近的工作日

      months: 0, // 选择月
      monthVal: '', // 提交月
      startMon: 1, // 周期开始月
      endMon: 2, // 周期结束月
      startMonth: 1, // 开始月
      intervalMonth: 1, // 间隔月
      checkMonth: [], // 指定月

      weeks: 0, // 选择周
      weekVal: '?', // 提交周
      startWeek: 1, // 周期开始周
      endWeek: 2, // 周期结束周
      startWeeks: 1, // 开始周
      intervalWeek: 1, // 间隔周
      checkWeek: [], // 指定周
      lastWeek: 1,

      years: 0, // 选择年
      yearVal: '', // 提交年
      startYear: '', // 周期开始年
      endYear: '', // 周期结束年

      currentYear: ''
    }
  },
  methods: {
    change (index) {
      this.showIndex = index
    },
    changeRadio (val) { // 选择秒
      this.seconds = val
      this.submit()
    },
    checkSeconds (val) { // 复选秒
      this.checkSecond = val
      if(this.checkSecond.length == 0) {
        this.secondVal = '?'
        this.cronParams = this.secondVal + ' ' + this.minuteVal + ' ' + this.hourVal + ' ' + this.dayVal + ' ' + this.monthVal + ' ' + this.weekVal + ' ' + this.yearVal
      } else {
          this.getSeconds()
      }
    },
    changeRadioMinute (val) { // 选择分
      this.minutes = val
      this.submit()
    },
    checkMinutes (val) { // 复选分
      this.checkMinute = val
      if(this.checkMinute.length == 0) {
        this.minuteVal = '?'
        this.cronParams = this.secondVal + ' ' + this.minuteVal + ' ' + this.hourVal + ' ' + this.dayVal + ' ' + this.monthVal + ' ' + this.weekVal + ' ' + this.yearVal
      } else {
          this.getMinutes()
      }
    },
    changeRadioHour (val) { // 选择时
      this.hours = val
      this.submit()
    },
    checkHours (val) { // 复选时
      this.checkHour = val
      if(this.checkHour.length == 0) {
        this.hourVal = '?'
        this.cronParams = this.secondVal + ' ' + this.minuteVal + ' ' + this.hourVal + ' ' + this.dayVal + ' ' + this.monthVal + ' ' + this.weekVal + ' ' + this.yearVal
      } else {
          this.getHours()
      }
    },
    changeRadioDay (val) { // 选择天
      this.days = val
      this.submit()
    },
    checkDays (val) { // 复选天
      this.checkDay = val
      if(this.checkDay.length == 0) {
        this.dayVal = '?'
        this.cronParams = this.secondVal + ' ' + this.minuteVal + ' ' + this.hourVal + ' ' + this.dayVal + ' ' + this.monthVal + ' ' + this.weekVal + ' ' + this.yearVal
      } else {
          this.getDays()
      }
    },
    changeRadioMonth (val) { // 选择月
      this.months = val
      this.submit()
    },
    checkMonths (val) { // 复选月
      this.checkMonth = val
      if(this.checkMonth.length == 0) {
        this.monthVal = '?'
        this.cronParams = this.secondVal + ' ' + this.minuteVal + ' ' + this.hourVal + ' ' + this.dayVal + ' ' + this.monthVal + ' ' + this.weekVal + ' ' + this.yearVal
      } else {
          this.getMonths()
      }
    },
    checkMonths (val) { // 复选月
      this.checkMonth = val
      if(this.checkMonth.length == 0) {
        this.monthVal = '?'
        this.cronParams = this.secondVal + ' ' + this.minuteVal + ' ' + this.hourVal + ' ' + this.dayVal + ' ' + this.monthVal + ' ' + this.weekVal + ' ' + this.yearVal
      } else {
          this.getMonths()
      }
    },
    changeRadioWeek (val) { // 选择周
      this.weeks = val
      this.submit()
    },
    checkWeeks (val) { // 复选周
      this.checkWeek = val
      if(this.checkWeek.length == 0) {
        this.weekVal = '?'
        this.cronParams = this.secondVal + ' ' + this.minuteVal + ' ' + this.hourVal + ' ' + this.dayVal + ' ' + this.monthVal + ' ' + this.weekVal + ' ' + this.yearVal
      } else {
          this.getWeeks()
      }
    },
    changeRadioYear (val) { // 选择年
      this.years = val
      this.submit()
    },
    getVal () { // 获取选择后的值
      // 秒
      if(this.seconds == 0) {
        this.secondVal = '*'
      }else if(this.seconds == 1) {
        this.secondVal = this.startSec + '-' + this.endSec
      } else if(this.seconds == 2) {
        this.secondVal = this.startSecond + '/' + this.intervalTime
      } else if(this.seconds == 3) {
        this.getSeconds()
      }

      // 分
      if(this.minutes == 0) {
        this.minuteVal = '*'
      }else if(this.minutes == 1) {
        if(this.secondVal == '*') {
          this.secondVal = '0'
        }
        this.minuteVal = this.startMin + '-' + this.endMin
      }else if(this.minutes == 2) {
        if(this.secondVal == '*') {
          this.secondVal = '0'
        }
        this.minuteVal = this.startMinute + '/' + this.intervalMinute
      } else if(this.minutes == 3) {
        if(this.secondVal == '*') {
          this.secondVal = '0'
        }
        this.getMinutes()
      }

      // 时
      if(this.hours == 0) {
        this.hourVal = '*'
      }else if(this.hours == 1) {
        if(this.secondVal == '*') {
          this.secondVal = '0'
        }
        if(this.minuteVal == '*') {
          this.minuteVal = '0'
        }
        this.hourVal = this.startHou + '-' + this.endHour
      }else if(this.hours == 2) {
        if(this.secondVal == '*') {
          this.secondVal = '0'
        }
        if(this.minuteVal == '*') {
          this.minuteVal = '0'
        }
        this.hourVal = this.startHour + '/' + this.intervalHour
      }else if(this.hours == 3) {
        if(this.secondVal == '*') {
          this.secondVal = '0'
        }
        if(this.minuteVal == '*') {
          this.minuteVal = '0'
        }
        this.getHours()
      }

      // 日
      if(this.days == 0) {
        this.dayVal = '*'
      }else if(this.days == 1) {
        if(this.secondVal == '*') {
          this.secondVal = '0'
        }
        if(this.minuteVal == '*') {
          this.minuteVal = '0'
        }
        if(this.hourVal == '*') {
          this.hourVal = '0'
        }

        this.dayVal = '?'
      }else if(this.days == 2) {
        if(this.secondVal == '*') {
          this.secondVal = '0'
        }
        if(this.minuteVal == '*') {
          this.minuteVal = '0'
        }
        if(this.hourVal == '*') {
          this.hourVal = '0'
        }

        this.dayVal = this.startDay + '-' + this.endDay
      }else if(this.days == 3) {
        if(this.secondVal == '*') {
          this.secondVal = '0'
        }
        if(this.minuteVal == '*') {
          this.minuteVal = '0'
        }
        if(this.hourVal == '*') {
          this.hourVal = '0'
        }

        this.dayVal = this.startDays + '/' + this.intervalDay
      }else if(this.days == 4) {
        if(this.secondVal == '*') {
          this.secondVal = '0'
        }
        if(this.minuteVal == '*') {
          this.minuteVal = '0'
        }
        if(this.hourVal == '*') {
          this.hourVal = '0'
        }

        this.dayVal = this.workDay + 'W'
      }else if(this.days == 5) {
        if(this.secondVal == '*') {
          this.secondVal = '0'
        }
        if(this.minuteVal == '*') {
          this.minuteVal = '0'
        }
        if(this.hourVal == '*') {
          this.hourVal = '0'
        }

        this.dayVal = 'L'
      }else if(this.days == 6) {
        if(this.secondVal == '*') {
          this.secondVal = '0'
        }
        if(this.minuteVal == '*') {
          this.minuteVal = '0'
        }
        if(this.hourVal == '*') {
          this.hourVal = '0'
        }

        this.getDays()
      }

      // 月
      if(this.months == 0) {
        this.monthVal = '*'
      }else if(this.months == 1) {
        if(this.secondVal == '*') {
          this.secondVal = '0'
        }
        if(this.minuteVal == '*') {
          this.minuteVal = '0'
        }
        if(this.hourVal == '*') {
          this.hourVal = '0'
        }
        if(this.dayVal == '*') {
          this.dayVal = '0'
        }

        this.monthVal = '?'
      }else if(this.months == 2) {
        if(this.secondVal == '*') {
          this.secondVal = '0'
        }
        if(this.minuteVal == '*') {
          this.minuteVal = '0'
        }
        if(this.hourVal == '*') {
          this.hourVal = '0'
        }
        if(this.dayVal == '*') {
          this.dayVal = '0'
        }

        this.monthVal = this.startMon + '-' + this.endMon
      }else if(this.months == 3) {
        if(this.secondVal == '*') {
          this.secondVal = '0'
        }
        if(this.minuteVal == '*') {
          this.minuteVal = '0'
        }
        if(this.hourVal == '*') {
          this.hourVal = '0'
        }
        if(this.dayVal == '*') {
          this.dayVal = '0'
        }

        this.monthVal = this.startMonth + '/' + this.intervalMonth
      }else if(this.months == 4) {
        if(this.secondVal == '*') {
          this.secondVal = '0'
        }
        if(this.minuteVal == '*') {
          this.minuteVal = '0'
        }
        if(this.hourVal == '*') {
          this.hourVal = '0'
        }
        if(this.dayVal == '*') {
          this.dayVal = '0'
        }

        this.getMonths()
      }

      // 周
      if(this.weeks == 0) {
        this.weekVal = '?'
      }else if(this.weeks == 1) {
        if(this.secondVal == '*') {
          this.secondVal = '0'
        }
        if(this.minuteVal == '*') {
          this.minuteVal = '0'
        }
        if(this.hourVal == '*') {
          this.hourVal = '0'
        }
        if(this.dayVal == '*') {
          this.dayVal = '0'
        }
        if(this.monthVal == '*') {
          this.monthVal = '0'
        }

        this.weekVal = '*'
      }else if(this.weeks == 2) {
        if(this.secondVal == '*') {
          this.secondVal = '0'
        }
        if(this.minuteVal == '*') {
          this.minuteVal = '0'
        }
        if(this.hourVal == '*') {
          this.hourVal = '0'
        }
        if(this.dayVal == '*') {
          this.dayVal = '0'
        }
        if(this.monthVal == '*') {
          this.monthVal = '0'
        }

        this.weekVal = this.startWeek + '-' + this.endWeek
      }else if(this.weeks == 3) {
        if(this.secondVal == '*') {
          this.secondVal = '0'
        }
        if(this.minuteVal == '*') {
          this.minuteVal = '0'
        }
        if(this.hourVal == '*') {
          this.hourVal = '0'
        }
        if(this.dayVal == '*') {
          this.dayVal = '0'
        }
        if(this.monthVal == '*') {
          this.monthVal = '0'
        }

        this.weekVal = this.startWeeks + '#' + this.intervalWeek
      }else if(this.weeks == 4) {
        if(this.secondVal == '*') {
          this.secondVal = '0'
        }
        if(this.minuteVal == '*') {
          this.minuteVal = '0'
        }
        if(this.hourVal == '*') {
          this.hourVal = '0'
        }
        if(this.dayVal == '*') {
          this.dayVal = '0'
        }
        if(this.monthVal == '*') {
          this.monthVal = '0'
        }

        this.weekVal = this.lastWeek + 'L'
      }else if(this.weeks == 5) {
        if(this.secondVal == '*') {
          this.secondVal = '0'
        }
        if(this.minuteVal == '*') {
          this.minuteVal = '0'
        }
        if(this.hourVal == '*') {
          this.hourVal = '0'
        }
        if(this.dayVal == '*') {
          this.dayVal = '0'
        }
        if(this.monthVal == '*') {
          this.monthVal = '0'
        }

        this.getWeeks()
      }

      // 年
      if(this.years == 0) {
        this.yearVal = ''
      }else if(this.years == 1) {
        if(this.secondVal == '*') {
          this.secondVal = '0'
        }
        if(this.minuteVal == '*') {
          this.minuteVal = '0'
        }
        if(this.hourVal == '*') {
          this.hourVal = '0'
        }
        if(this.dayVal == '*') {
          this.dayVal = '0'
        }
        if(this.monthVal == '*') {
          this.monthVal = '0'
        }

        this.yearVal = '*'
      }else if(this.years == 2) {
        if(this.secondVal == '*') {
          this.secondVal = '0'
        }
        if(this.minuteVal == '*') {
          this.minuteVal = '0'
        }
        if(this.hourVal == '*') {
          this.hourVal = '0'
        }
        if(this.dayVal == '*') {
          this.dayVal = '0'
        }
        if(this.monthVal == '*') {
          this.monthVal = '0'
        }

        this.yearVal = this.startYear + '-' + this.endYear
      }

      this.cronParams = this.secondVal + ' ' + this.minuteVal + ' ' + this.hourVal + ' ' + this.dayVal + ' ' + this.monthVal + ' ' + this.weekVal + ' ' + this.yearVal

    },
    submit () {
      this.getVal()
      this.cronParams = this.secondVal + ' ' + this.minuteVal + ' ' + this.hourVal + ' ' + this.dayVal + ' ' + this.monthVal + ' ' + this.weekVal + ' ' + this.yearVal
    },
    // 获取当前年
    getCurrent () {
      let current = new Date()
      this.currentYear = current.getFullYear()
      this.startYear = current.getFullYear()
      this.endYear = this.startYear + 1
    },
    // 获取秒
    getSeconds () {
      let arr = []
      let str = 0
      let obj = ''
      if(this.checkSecond.length == 0) {
        this.secondVal = '?'
      } else {
        for(let i = 0; i < this.checkSecond.length; i++) {
          str = parseInt(this.checkSecond[i])
          arr.push(str)
        }
        for(let j = 0; j < arr.length; j++) {
          obj += arr[j] + ','
        }
        this.secondVal = obj.substring(0, obj.length - 1)
      }

      this.cronParams = this.secondVal + ' ' + this.minuteVal + ' ' + this.hourVal + ' ' + this.dayVal + ' ' + this.monthVal + ' ' + this.weekVal + ' ' + this.yearVal
    },
    // 获取分
    getMinutes () {
      let arr = []
      let str = 0
      let obj = ''
      if(this.checkMinute.length == 0) {
        this.minuteVal = '?'
      } else {
        for(let i = 0; i < this.checkMinute.length; i++) {
          str = parseInt(this.checkMinute[i])
          arr.push(str)
        }
        for(let j = 0; j < arr.length; j++) {
          obj += arr[j] + ','
        }
        this.minuteVal = obj.substring(0, obj.length - 1)
      }
      this.cronParams = this.secondVal + ' ' + this.minuteVal + ' ' + this.hourVal + ' ' + this.dayVal + ' ' + this.monthVal + ' ' + this.weekVal + ' ' + this.yearVal
    },
    // 获取时
    getHours () {
      let arr = []
      let str = 0
      let obj = ''
      if(this.checkHour.length == 0) {
        this.hourVal = '?'
      } else {
        for(let i = 0; i < this.checkHour.length; i++) {
          str = parseInt(this.checkHour[i])
          arr.push(str)
        }
        for(let j = 0; j < arr.length; j++) {
          obj += arr[j] + ','
        }
        this.hourVal = obj.substring(0, obj.length - 1)
      }
      this.cronParams = this.secondVal + ' ' + this.minuteVal + ' ' + this.hourVal + ' ' + this.dayVal + ' ' + this.monthVal + ' ' + this.weekVal + ' ' + this.yearVal
    },
    // 获取天
    getDays () {
      let arr = []
      let str = 0
      let obj = ''
      if(this.checkDay.length == 0) {
        this.dayVal = '?'
      } else {
        for(let i = 0; i < this.checkDay.length; i++) {
          str = parseInt(this.checkDay[i])
          arr.push(str)
        }
        for(let j = 0; j < arr.length; j++) {
          obj += arr[j] + ','
        }
        this.dayVal = obj.substring(0, obj.length - 1)
      }
      this.cronParams = this.secondVal + ' ' + this.minuteVal + ' ' + this.hourVal + ' ' + this.dayVal + ' ' + this.monthVal + ' ' + this.weekVal + ' ' + this.yearVal
    },
    // 获取月
    getMonths () {
      let arr = []
      let str = 0
      let obj = ''
      if(this.checkMonth.length == 0) {
        this.monthVal = '?'
      } else {
        for(let i = 0; i < this.checkMonth.length; i++) {
          str = parseInt(this.checkMonth[i])
          arr.push(str)
        }
        for(let j = 0; j < arr.length; j++) {
          obj += arr[j] + ','
        }
        this.monthVal = obj.substring(0, obj.length - 1)
      }
      this.cronParams = this.secondVal + ' ' + this.minuteVal + ' ' + this.hourVal + ' ' + this.dayVal + ' ' + this.monthVal + ' ' + this.weekVal + ' ' + this.yearVal
    },
    // 获取周
    getWeeks () {
      let arr = []
      let str = 0
      let obj = ''
      if(this.checkWeek.length == 0) {
        this.weekVal = '?'
      } else {
        for(let i = 0; i < this.checkWeek.length; i++) {
          str = parseInt(this.checkWeek[i])
          arr.push(str)
        }
        for(let j = 0; j < arr.length; j++) {
          obj += arr[j] + ','
        }
        this.weekVal = obj.substring(0, obj.length - 1)
      }
      this.cronParams = this.secondVal + ' ' + this.minuteVal + ' ' + this.hourVal + ' ' + this.dayVal + ' ' + this.monthVal + ' ' + this.weekVal + ' ' + this.yearVal
    },
    reset () {
      this.showIndex = 0
      this.secondVal = '*'
      this.minuteVal = '*'
      this.hourVal = '*'
      this.dayVal = '*'
      this.monthVal = '*'
      this.weekVal = '?'
      this.yearVal = ''
      this.cronParams = this.secondVal + ' ' + this.minuteVal + ' ' + this.hourVal + ' ' + this.dayVal + ' ' + this.monthVal + ' ' + this.weekVal + ' ' + this.yearVal
    }
  },
  mounted () {
    this.changeRadio(0)
    this.changeRadioMinute(0)
    this.changeRadioHour(0)
    this.changeRadioDay(0)
    this.changeRadioMonth(0)
    this.changeRadioWeek(0)
    this.changeRadioYear(0)
    this.getCurrent()
  }
}
</script>

<style lang="less">
@bgBackground: #409fff;
@hoverBackground: #094f95;
@title: #ff0;
.tab-container {
  // height: 100%;
  width: 100%;
  border: 1px solid #ff0;
  margin: 0 auto;
  .contents {
    // height: 100%;
    // width: 100%;
    font-size: 16px;
    // tab栏样式
    .title {
      // height: 7%;
      line-height: 7vh;
      box-sizing: border-box;

      >.el-col-3 {
        cursor: pointer;
        text-align: center;
        border-right: 1px solid #ccc;
        border-bottom: 1px solid #ccc;

      }
    }

    // 主体内容部分样式
    .main {
      // width: 83.5%;
      // height: 70%;
      margin-top: 2px;
      border-right: 1px solid #ccc;
      border-bottom: 1px solid #ccc;
      margin: 0 auto;
      .minutes {
        text-align: left;
        margin-left: 30px;
        // height: 100%;
        > .el-row {
          height: 50px;
          border-bottom: 1px solid #ccc;
          line-height: 49px;
          box-sizing: border-box;
          .el-col-1 {
            .el-radio {
              .el-radio__label {
                display: none!important;
              }
            }
          }

          .el-col-16 {
            // height: 100%;
            .nums {
              width: 10%;
            }
          }
        }
      }

    }

    .footer {
      margin-top: 10px;
    }

    // 公共样式
    .active {
      border-bottom: none!important;
    }

    .el-checkbox+.el-checkbox {
      margin-left: 0;
    }
   
  }
}
</style>
