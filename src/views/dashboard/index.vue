<template>
  <div class="dashboard-container">
    <h1>Biểu mẫu tự đánh giá</h1>
    <strong>Current point: {{ totalCaculatePoint }}</strong>
    <table>
      <thead>
        <tr>
          <th rowspan="2">Main Fators</th>
          <th rowspan="2">Weight</th>
          <th rowspan="2">Addition factors</th>
          <th rowspan="2">Maximum Level</th>
          <th rowspan="2">Maximum Score Group</th>
          <th rowspan="2">Maximum Score</th>
          <!--          <th colspan="5">Degree Evaluation</th>-->
          <th rowspan="2">Degree Evaluation</th>
          <th rowspan="2">Note</th>
        </tr>
        <!--        <tr>-->
        <!--          <td>Không biết</td>-->
        <!--          <td>Cơ bản</td>-->
        <!--          <td>Sơ cấp</td>-->
        <!--          <td>Trung cấp</td>-->
        <!--          <td>Cao cấp</td>-->
        <!--        </tr>-->
      </thead>
      <template v-for="(item, index) in parentAndChildData">
        <!--        <TrRecursive :question="item" :children-recursive="item.children_recursive" />-->
        <template v-if="item.children_recursive.length">
          <tr v-for="(itemChild, indexChild) in item.children_recursive" :key="`${indexChild}${index}`">
            <td v-if="indexChild === 0 || item.id !== itemChild.parent_id" :rowspan="item.children_recursive.length">{{ item.content.vn }} </td>
            <td v-if="indexChild === 0 || item.id !== itemChild.parent_id" :rowspan="item.children_recursive.length">{{ item.proportionMain }}%</td>
            <td>{{ JSON.parse(itemChild.content).en }}</td>
            <td>{{ itemChild.max_level }}</td>
            <td>{{ itemChild.max_score_group }}</td>
            <td>{{ itemChild.max_score }}</td>
            <td v-if="item.type === 1">
              <div v-for="level in Number(itemChild.max_level)" :key="`level${level}`">
                <el-radio v-model="yourAnswers[`${itemChild.parent_id}_${itemChild.id}`].your_answer" :label="level" @change="changeAnswer(`${itemChild.parent_id}_${itemChild.id}`)"> {{ levelText[Number(level)] }} </el-radio>
              </div>
            </td>
            <td v-else>
              <el-input
                v-model="yourAnswers[`${itemChild.parent_id}_${itemChild.id}`].your_answer"
                :rows="2"
                type="textarea"
                placeholder="Your answer"
              />
            </td>
            <!--            <td>-->
            <!--              <el-radio v-model="yourAnswers[`${itemChild.parent_id}_${itemChild.id}`].your_answer" label="2" />-->
            <!--            </td>-->
            <!--            <td>-->
            <!--              <el-radio v-model="yourAnswers[`${itemChild.parent_id}_${itemChild.id}`].your_answer" label="2" />-->
            <!--            </td>-->
            <!--            <td>-->
            <!--              <el-radio v-model="yourAnswers[`${itemChild.parent_id}_${itemChild.id}`].your_answer" label="3" />-->
            <!--            </td>-->
            <!--            <td>-->
            <!--              <el-radio v-model="yourAnswers[`${itemChild.parent_id}_${itemChild.id}`].your_answer" label="4" />-->
            <!--            </td>-->
            <!--            <td>-->
            <!--              <el-radio v-model="yourAnswers[`${itemChild.parent_id}_${itemChild.id}`].your_answer" label="5" />-->
            <!--            </td>-->
            <td>
              <el-input
                v-model="yourAnswers[`${itemChild.parent_id}_${itemChild.id}`].note"
                :rows="2"
                type="textarea"
                placeholder="Your note"
              />
            </td>
          </tr>
        </template>
      </template>
    </table>
    <h1>Biểu mẫu test</h1>
    <table>
      <thead>
        <tr>
          <th rowspan="2">Main Fators</th>
          <th rowspan="2">Weight</th>
          <th rowspan="2">Addition factors</th>
          <th rowspan="2">Maximum Level</th>
          <th rowspan="2">Maximum Score Group</th>
          <th rowspan="2">Maximum Score</th>
          <th colspan="5">Degree Evaluation</th>
          <th rowspan="2">Note</th>
        </tr>
        <tr>
          <td>Không biết</td>
          <td>Cơ bản</td>
          <td>Sơ cấp</td>
          <td>Trung cấp</td>
          <td>Cao cấp</td>
        </tr>
      </thead>
      <tr>
        <td rowspan="4">Tuân thủ nội quy công ty </td>
        <td rowspan="4">10%</td>
        <td rowspan="2">Phân tích yêu cầu 1</td>
        <td>Phân tích yêu cầu 1.1</td>
        <td>5</td>
        <td>10</td>
        <td><label role="radio" tabindex="0" class="el-radio"><span class="el-radio__input"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="1"></span><span class="el-radio__label">1</span></label></td>
        <td><label role="radio" tabindex="0" class="el-radio is-checked" aria-checked="true"><span class="el-radio__input is-checked"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="2"></span><span class="el-radio__label">2</span></label></td>
        <td><label role="radio" tabindex="0" class="el-radio"><span class="el-radio__input"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="3"></span><span class="el-radio__label">3</span></label></td>
        <td><label role="radio" tabindex="0" class="el-radio"><span class="el-radio__input"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="4"></span><span class="el-radio__label">4</span></label></td>
        <td><label role="radio" tabindex="0" class="el-radio"><span class="el-radio__input"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="5"></span><span class="el-radio__label">5</span></label></td>
        <td>
          <div class="el-textarea el-input--medium">
            <textarea autocomplete="off" rows="2" placeholder="Your note" class="el-textarea__inner" style="min-height: 33.2222px;" />
            <!---->
          </div>
        </td>
      </tr>
      <tr>
        <!----><!---->
        <td>Phân tích yêu cầu 1.2</td>
        <td>5</td>
        <td>10</td>
        <td><label role="radio" tabindex="0" class="el-radio"><span class="el-radio__input"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="1"></span><span class="el-radio__label">1</span></label></td>
        <td><label role="radio" tabindex="0" class="el-radio is-checked" aria-checked="true"><span class="el-radio__input is-checked"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="2"></span><span class="el-radio__label">2</span></label></td>
        <td><label role="radio" tabindex="0" class="el-radio"><span class="el-radio__input"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="3"></span><span class="el-radio__label">3</span></label></td>
        <td><label role="radio" tabindex="0" class="el-radio"><span class="el-radio__input"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="4"></span><span class="el-radio__label">4</span></label></td>
        <td><label role="radio" tabindex="0" class="el-radio"><span class="el-radio__input"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="5"></span><span class="el-radio__label">5</span></label></td>
        <td>
          <div class="el-textarea el-input--medium">
            <textarea autocomplete="off" rows="2" placeholder="Your note" class="el-textarea__inner" style="min-height: 33.2222px;" />
            <!---->
          </div>
        </td>
      </tr>
      <tr>
        <!----><!---->
        <td>Phân tích yêu cầu 3</td>
        <td>10</td>
        <td>5</td>
        <td>10</td>
        <td><label role="radio" tabindex="0" class="el-radio"><span class="el-radio__input"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="1"></span><span class="el-radio__label">1</span></label></td>
        <td><label role="radio" tabindex="0" class="el-radio is-checked" aria-checked="true"><span class="el-radio__input is-checked"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="2"></span><span class="el-radio__label">2</span></label></td>
        <td><label role="radio" tabindex="0" class="el-radio"><span class="el-radio__input"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="3"></span><span class="el-radio__label">3</span></label></td>
        <td><label role="radio" tabindex="0" class="el-radio"><span class="el-radio__input"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="4"></span><span class="el-radio__label">4</span></label></td>
        <td><label role="radio" tabindex="0" class="el-radio"><span class="el-radio__input"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="5"></span><span class="el-radio__label">5</span></label></td>
        <td>
          <div class="el-textarea el-input--medium">
            <textarea autocomplete="off" rows="2" placeholder="Your note" class="el-textarea__inner" style="min-height: 33.2222px;" />
            <!---->
          </div>
        </td>
      </tr>
      <tr>
        <!----><!---->
        <td>Phân tích yêu cầu 4</td>
        <td>10</td>
        <td>5</td>
        <td>10</td>
        <td><label role="radio" tabindex="0" class="el-radio is-checked" aria-checked="true"><span class="el-radio__input is-checked"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="1"></span><span class="el-radio__label">1</span></label></td>
        <td><label role="radio" tabindex="0" class="el-radio"><span class="el-radio__input"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="2"></span><span class="el-radio__label">2</span></label></td>
        <td><label role="radio" tabindex="0" class="el-radio"><span class="el-radio__input"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="3"></span><span class="el-radio__label">3</span></label></td>
        <td><label role="radio" tabindex="0" class="el-radio"><span class="el-radio__input"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="4"></span><span class="el-radio__label">4</span></label></td>
        <td><label role="radio" tabindex="0" class="el-radio"><span class="el-radio__input"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="5"></span><span class="el-radio__label">5</span></label></td>
        <td>
          <div class="el-textarea el-input--medium">
            <textarea autocomplete="off" rows="2" placeholder="Your note" class="el-textarea__inner" style="min-height: 33.2222px;" />
            <!---->
          </div>
        </td>
      </tr>
      <tr>
        <td rowspan="2">Phân tích yêu cầu phần mềm </td>
        <td rowspan="2">10%</td>
        <td>Phân tích yêu cầu</td>
        <td>10</td>
        <td>5</td>
        <td>10</td>
        <td><label role="radio" tabindex="0" class="el-radio"><span class="el-radio__input"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="1"></span><span class="el-radio__label">1</span></label></td>
        <td><label role="radio" tabindex="0" class="el-radio"><span class="el-radio__input"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="2"></span><span class="el-radio__label">2</span></label></td>
        <td><label role="radio" tabindex="0" class="el-radio"><span class="el-radio__input"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="3"></span><span class="el-radio__label">3</span></label></td>
        <td><label role="radio" tabindex="0" class="el-radio is-checked" aria-checked="true"><span class="el-radio__input is-checked"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="4"></span><span class="el-radio__label">4</span></label></td>
        <td><label role="radio" tabindex="0" class="el-radio"><span class="el-radio__input"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="5"></span><span class="el-radio__label">5</span></label></td>
        <td>
          <div class="el-textarea el-input--medium">
            <textarea autocomplete="off" rows="2" placeholder="Your note" class="el-textarea__inner" style="min-height: 33.2222px;" />
            <!---->
          </div>
        </td>
      </tr>
      <tr>
        <!----><!---->
        <td>Ước lượng và lập kế hoạch</td>
        <td>10</td>
        <td>5</td>
        <td>10</td>
        <td><label role="radio" tabindex="0" class="el-radio"><span class="el-radio__input"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="1"></span><span class="el-radio__label">1</span></label></td>
        <td><label role="radio" tabindex="0" class="el-radio"><span class="el-radio__input"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="2"></span><span class="el-radio__label">2</span></label></td>
        <td><label role="radio" tabindex="0" class="el-radio"><span class="el-radio__input"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="3"></span><span class="el-radio__label">3</span></label></td>
        <td><label role="radio" tabindex="0" class="el-radio is-checked" aria-checked="true"><span class="el-radio__input is-checked"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="4"></span><span class="el-radio__label">4</span></label></td>
        <td><label role="radio" tabindex="0" class="el-radio"><span class="el-radio__input"><span class="el-radio__inner" /><input type="radio" aria-hidden="true" tabindex="-1" class="el-radio__original" value="5"></span><span class="el-radio__label">5</span></label></td>
        <td>
          <div class="el-textarea el-input--medium">
            <textarea autocomplete="off" rows="2" placeholder="Your note" class="el-textarea__inner" style="min-height: 33.2222px;" />
            <!---->
          </div>
        </td>
      </tr>
    </table>
    <h1>Xem kết quả tự đánh giá</h1>
    <table>
      <thead>
        <tr>
          <th rowspan="2">Main Fators</th>
          <th rowspan="2">Weight</th>
          <th rowspan="2">Addition factors</th>
          <th rowspan="2">Maximum Level</th>
          <th rowspan="2">Maximum Score Group</th>
          <th rowspan="2">Maximum Score</th>
          <th rowspan="2">Degree Evaluation</th>
          <th rowspan="2">Note</th>
        </tr>
      </thead>
      <TrRecursive1 :children-recursive="questions" />
    </table>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import adminDashboard from './admin'
import editorDashboard from './editor'
import TrRecursive from '@/components/TrRecursive'
import TrRecursive1 from '@/components/TrRecursive/index1'
export default {
  name: 'Dashboard',
  components: { adminDashboard, editorDashboard, TrRecursive, TrRecursive1 },
  data() {
    return {
      levelText: {
        1: 'Không biêt',
        2: 'Cơ bản',
        3: 'Sơ cấp',
        4: 'Trung cấp',
        5: 'Cao cấp'
      },
      currentRole: 'adminDashboard',
      dataTable: [
        {
          'id': 133,
          'question_weight': null,
          'point': null,
          'proportionMain': '10',
          'proportionExtra': '10',
          'maxPoint': '10',
          'content': {
            'en': 'Tuân thủ nội quy công ty',
            'ja': 'Tuân thủ nội quy công ty',
            'vn': 'Tuân thủ nội quy công ty'
          },
          'tag_name': null,
          'versions': 1,
          'deleted_at': null,
          'created_at': '2023-05-23T02:08:28.000000Z',
          'updated_at': '2023-05-23T02:08:28.000000Z',
          'type': 1,
          'parent_id': null,
          'order': null,
          'explain': '{"en": "Tuân thủ nội quy công ty", "ja": "Tuân thủ nội quy công ty", "vn": "Tuân thủ nội quy công ty"}',
          'categories': [
            {
              'id': 1,
              'name': 'Thái độ',
              'pivot': {
                'question_id': 133,
                'category_id': 1,
                'created_at': '2023-05-23T02:08:28.000000Z',
                'updated_at': '2023-05-23T02:08:28.000000Z',
                'deleted_at': null
              }
            }
          ],
          'children_recursive': [
            {
              'id': 128,
              'content': '{"en": "Phân tích yêu cầu 1", "ja": "Phân tích yêu cầu", "vn": "Phân tích yêu cầu"}',
              'tag_name': null,
              'versions': 1,
              'deleted_at': null,
              'created_at': '2023-05-23T02:00:08.000000Z',
              'updated_at': '2023-05-23T02:00:08.000000Z',
              'type': 1,
              'parent_id': 133,
              'order': null,
              'explain': '{"en": "Phân tích yêu cầu", "ja": "Phân tích yêu cầu", "vn": "Phân tích yêu cầu"}',
              'children_recursive': [],
              'categories': [
                {
                  'id': 2,
                  'name': 'Kĩ năng/Kiến thức',
                  'deleted_at': null,
                  'created_at': '2023-05-18T09:29:13.000000Z',
                  'updated_at': '2023-05-19T10:12:40.000000Z',
                  'pivot': {
                    'question_id': 128,
                    'category_id': 2,
                    'created_at': '2023-05-23T02:00:08.000000Z',
                    'updated_at': '2023-05-23T02:00:08.000000Z',
                    'deleted_at': null
                  }
                }
              ],
              'max_level': '5',
              'max_score_group': '10',
              'proportion': '10',
              'max_score': '10'
            },
            {
              'id': 129,
              'content': '{"en": "Phân tích yêu cầu 2", "ja": "Phân tích yêu cầu", "vn": "Phân tích yêu cầu"}',
              'tag_name': null,
              'versions': 1,
              'deleted_at': null,
              'created_at': '2023-05-23T02:00:08.000000Z',
              'updated_at': '2023-05-23T02:00:08.000000Z',
              'type': 1,
              'parent_id': 133,
              'order': null,
              'explain': '{"en": "Phân tích yêu cầu", "ja": "Phân tích yêu cầu", "vn": "Phân tích yêu cầu"}',
              'children_recursive': [
                {
                  'id': 1,
                  'content': '{"en": "Phân tích yêu cầu con", "ja": "Phân tích yêu cầu", "vn": "Phân tích yêu cầu con"}',
                  'tag_name': null,
                  'versions': 1,
                  'deleted_at': null,
                  'created_at': '2023-05-23T02:00:08.000000Z',
                  'updated_at': '2023-05-23T02:00:08.000000Z',
                  'type': 1,
                  'parent_id': 128,
                  'order': null,
                  'explain': '{"en": "Phân tích yêu cầu", "ja": "Phân tích yêu cầu", "vn": "Phân tích yêu cầu"}',
                  'children_recursive': [],
                  'categories': [
                    {
                      'id': 2,
                      'name': 'Kĩ năng/Kiến thức',
                      'deleted_at': null,
                      'created_at': '2023-05-18T09:29:13.000000Z',
                      'updated_at': '2023-05-19T10:12:40.000000Z',
                      'pivot': {
                        'question_id': 128,
                        'category_id': 2,
                        'created_at': '2023-05-23T02:00:08.000000Z',
                        'updated_at': '2023-05-23T02:00:08.000000Z',
                        'deleted_at': null
                      }
                    }
                  ],
                  'max_level': '5',
                  'max_score_group': '10',
                  'proportion': '10',
                  'max_score': '10'
                }
              ],
              'categories': [
                {
                  'id': 2,
                  'name': 'Kĩ năng/Kiến thức',
                  'deleted_at': null,
                  'created_at': '2023-05-18T09:29:13.000000Z',
                  'updated_at': '2023-05-19T10:12:40.000000Z',
                  'pivot': {
                    'question_id': 128,
                    'category_id': 2,
                    'created_at': '2023-05-23T02:00:08.000000Z',
                    'updated_at': '2023-05-23T02:00:08.000000Z',
                    'deleted_at': null
                  }
                }
              ],
              'max_level': '5',
              'max_score_group': '10',
              'proportion': '10',
              'max_score': '10'
            },
            {
              'id': 130,
              'content': '{"en": "Phân tích yêu cầu 3", "ja": "Phân tích yêu cầu", "vn": "Phân tích yêu cầu"}',
              'tag_name': null,
              'versions': 1,
              'deleted_at': null,
              'created_at': '2023-05-23T02:00:08.000000Z',
              'updated_at': '2023-05-23T02:00:08.000000Z',
              'type': 1,
              'parent_id': 133,
              'order': null,
              'explain': '{"en": "Phân tích yêu cầu", "ja": "Phân tích yêu cầu", "vn": "Phân tích yêu cầu"}',
              'children_recursive': [],
              'categories': [
                {
                  'id': 2,
                  'name': 'Kĩ năng/Kiến thức',
                  'deleted_at': null,
                  'created_at': '2023-05-18T09:29:13.000000Z',
                  'updated_at': '2023-05-19T10:12:40.000000Z',
                  'pivot': {
                    'question_id': 128,
                    'category_id': 2,
                    'created_at': '2023-05-23T02:00:08.000000Z',
                    'updated_at': '2023-05-23T02:00:08.000000Z',
                    'deleted_at': null
                  }
                }
              ],
              'max_level': '5',
              'max_score_group': '10',
              'proportion': '10',
              'max_score': '10'
            },
            {
              'id': 131,
              'content': '{"en": "Phân tích yêu cầu 4", "ja": "Phân tích yêu cầu", "vn": "Phân tích yêu cầu"}',
              'tag_name': null,
              'versions': 1,
              'deleted_at': null,
              'created_at': '2023-05-23T02:00:08.000000Z',
              'updated_at': '2023-05-23T02:00:08.000000Z',
              'type': 1,
              'parent_id': 133,
              'order': null,
              'explain': '{"en": "Phân tích yêu cầu", "ja": "Phân tích yêu cầu", "vn": "Phân tích yêu cầu"}',
              'children_recursive': [],
              'categories': [
                {
                  'id': 2,
                  'name': 'Kĩ năng/Kiến thức',
                  'deleted_at': null,
                  'created_at': '2023-05-18T09:29:13.000000Z',
                  'updated_at': '2023-05-19T10:12:40.000000Z',
                  'pivot': {
                    'question_id': 128,
                    'category_id': 2,
                    'created_at': '2023-05-23T02:00:08.000000Z',
                    'updated_at': '2023-05-23T02:00:08.000000Z',
                    'deleted_at': null
                  }
                }
              ],
              'max_level': '5',
              'max_score_group': '10',
              'proportion': '10',
              'max_score': '10'
            }
          ]
        },
        {
          'id': 127,
          'question_weight': null,
          'point': null,
          'proportionMain': '10',
          'proportionExtra': '10',
          'maxPoint': '10',
          'content': {
            'en': 'Phân tích yêu cầu phần mềm',
            'ja': 'Phân tích yêu cầu phần mềm',
            'vn': 'Phân tích yêu cầu phần mềm'
          },
          'tag_name': null,
          'versions': 1,
          'deleted_at': null,
          'created_at': '2023-05-23T01:59:44.000000Z',
          'updated_at': '2023-05-23T01:59:44.000000Z',
          'type': 0,
          'parent_id': null,
          'order': null,
          'explain': '{"en": "Phân tích yêu cầu phần mềm", "ja": "Phân tích yêu cầu phần mềm", "vn": "Phân tích yêu cầu phần mềm"}',
          'categories': [
            {
              'id': 2,
              'name': 'Kĩ năng/Kiến thức',
              'pivot': {
                'question_id': 127,
                'category_id': 2,
                'created_at': '2023-05-23T01:59:44.000000Z',
                'updated_at': '2023-05-23T01:59:44.000000Z',
                'deleted_at': null
              }
            }
          ],
          'children_recursive': [
            {
              'id': 132,
              'content': '{"en": "Phân tích yêu cầu", "ja": "Phân tích yêu cầu", "vn": "Phân tích yêu cầu"}',
              'tag_name': null,
              'versions': 1,
              'deleted_at': null,
              'created_at': '2023-05-23T02:00:08.000000Z',
              'updated_at': '2023-05-23T02:00:08.000000Z',
              'type': 1,
              'parent_id': 127,
              'order': null,
              'explain': '{"en": "Phân tích yêu cầu", "ja": "Phân tích yêu cầu", "vn": "Phân tích yêu cầu"}',
              'children_recursive': [],
              'categories': [
                {
                  'id': 2,
                  'name': 'Kĩ năng/Kiến thức',
                  'deleted_at': null,
                  'created_at': '2023-05-18T09:29:13.000000Z',
                  'updated_at': '2023-05-19T10:12:40.000000Z',
                  'pivot': {
                    'question_id': 128,
                    'category_id': 2,
                    'created_at': '2023-05-23T02:00:08.000000Z',
                    'updated_at': '2023-05-23T02:00:08.000000Z',
                    'deleted_at': null
                  }
                }
              ],
              'max_level': '5',
              'max_score_group': '10',
              'proportion': '10',
              'max_score': '10'
            },
            {
              'id': 134,
              'content': '{"en": "Ước lượng và lập kế hoạch", "ja": "Ước lượng và lập kế hoạch", "vn": "Ước lượng và lập kế hoạch"}',
              'tag_name': null,
              'versions': 1,
              'deleted_at': null,
              'created_at': '2023-05-23T02:00:22.000000Z',
              'updated_at': '2023-05-23T02:00:22.000000Z',
              'type': 1,
              'parent_id': 127,
              'order': null,
              'explain': '{"en": "Ước lượng và lập kế hoạch", "ja": "Ước lượng và lập kế hoạch", "vn": "Ước lượng và lập kế hoạch"}',
              'children_recursive': [],
              'categories': [
                {
                  'id': 2,
                  'name': 'Kĩ năng/Kiến thức',
                  'deleted_at': null,
                  'created_at': '2023-05-18T09:29:13.000000Z',
                  'updated_at': '2023-05-19T10:12:40.000000Z',
                  'pivot': {
                    'question_id': 129,
                    'category_id': 2,
                    'created_at': '2023-05-23T02:00:22.000000Z',
                    'updated_at': '2023-05-23T02:00:22.000000Z',
                    'deleted_at': null
                  }
                }
              ],
              'max_level': '5',
              'max_score_group': '10',
              'proportion': '10',
              'max_score': '10'
            }
          ]
        }
      ],
      parentAndChildData: [],
      yourAnswers: [],
      questions: [
        {
          'id': 133,
          'question_weight': null,
          'point': null,
          'proportionMain': '10',
          'proportionExtra': '10',
          'maxPoint': '10',
          'content': {
            'en': 'Tuân thủ nội quy công ty',
            'ja': 'Tuân thủ nội quy công ty',
            'vn': 'Tuân thủ nội quy công ty'
          },
          'tag_name': null,
          'versions': 1,
          'deleted_at': null,
          'created_at': '2023-05-23T02:08:28.000000Z',
          'updated_at': '2023-05-23T02:08:28.000000Z',
          'type': 1,
          'parent_id': null,
          'order': null,
          'explain': '{"en": "Tuân thủ nội quy công ty", "ja": "Tuân thủ nội quy công ty", "vn": "Tuân thủ nội quy công ty"}',
          'categories': [
            {
              'id': 1,
              'name': 'Thái độ',
              'pivot': {
                'question_id': 133,
                'category_id': 1,
                'created_at': '2023-05-23T02:08:28.000000Z',
                'updated_at': '2023-05-23T02:08:28.000000Z',
                'deleted_at': null
              }
            }
          ],
          'children_recursive': [],
          'parent': {
            'id': 135,
            'content': '{"en": "Phân tích yêu cầu phần mềm", "ja": "Phân tích yêu cầu phần mềm", "vn": "Phân tích yêu cầu phần mềm"}',
            'tag_name': null,
            'versions': 1,
            'deleted_at': null,
            'created_at': '2023-05-23T01:59:44.000000Z',
            'updated_at': '2023-05-23T01:59:44.000000Z',
            'type': 1,
            'parent_id': null,
            'order': null,
            'explain': '{"en": "Phân tích yêu cầu phần mềm", "ja": "Phân tích yêu cầu phần mềm", "vn": "Phân tích yêu cầu phần mềm"}'
          }
        },
        {
          'id': 127,
          'question_weight': null,
          'point': null,
          'proportionMain': '10',
          'proportionExtra': '10',
          'maxPoint': '10',
          'content': {
            'en': 'Phân tích yêu cầu phần mềm',
            'ja': 'Phân tích yêu cầu phần mềm',
            'vn': 'Phân tích yêu cầu phần mềm'
          },
          'tag_name': null,
          'versions': 1,
          'deleted_at': null,
          'created_at': '2023-05-23T01:59:44.000000Z',
          'updated_at': '2023-05-23T01:59:44.000000Z',
          'type': 1,
          'parent_id': null,
          'order': null,
          'explain': '{"en": "Phân tích yêu cầu phần mềm", "ja": "Phân tích yêu cầu phần mềm", "vn": "Phân tích yêu cầu phần mềm"}',
          'categories': [
            {
              'id': 2,
              'name': 'Kĩ năng/Kiến thức',
              'pivot': {
                'question_id': 127,
                'category_id': 2,
                'created_at': '2023-05-23T01:59:44.000000Z',
                'updated_at': '2023-05-23T01:59:44.000000Z',
                'deleted_at': null
              }
            }
          ],
          'parent': {
            'id': 134,
            'content': '{"en": "Phân tích yêu cầu phần mềm", "ja": "Phân tích yêu cầu phần mềm", "vn": "Phân tích yêu cầu phần mềm"}',
            'tag_name': null,
            'versions': 1,
            'deleted_at': null,
            'created_at': '2023-05-23T01:59:44.000000Z',
            'updated_at': '2023-05-23T01:59:44.000000Z',
            'type': 1,
            'parent_id': null,
            'order': null,
            'explain': '{"en": "Phân tích yêu cầu phần mềm", "ja": "Phân tích yêu cầu phần mềm", "vn": "Phân tích yêu cầu phần mềm"}'
          },
          'children_recursive': []
        },
        {
          'id': 128,
          'content': '{"en": "Phân tích yêu cầu", "ja": "Phân tích yêu cầu", "vn": "Phân tích yêu cầu"}',
          'tag_name': null,
          'versions': 1,
          'deleted_at': null,
          'created_at': '2023-05-23T02:00:08.000000Z',
          'updated_at': '2023-05-23T02:00:08.000000Z',
          'type': 1,
          'parent_id': 127,
          'order': null,
          'explain': '{"en": "Phân tích yêu cầu", "ja": "Phân tích yêu cầu", "vn": "Phân tích yêu cầu"}',
          'children_recursive': [],
          'categories': [
            {
              'id': 2,
              'name': 'Kĩ năng/Kiến thức',
              'deleted_at': null,
              'created_at': '2023-05-18T09:29:13.000000Z',
              'updated_at': '2023-05-19T10:12:40.000000Z',
              'pivot': {
                'question_id': 128,
                'category_id': 2,
                'created_at': '2023-05-23T02:00:08.000000Z',
                'updated_at': '2023-05-23T02:00:08.000000Z',
                'deleted_at': null
              }
            }
          ],
          'parent': {
            'id': 134,
            'content': '{"en": "Phân tích yêu cầu phần mềm", "ja": "Phân tích yêu cầu phần mềm", "vn": "Phân tích yêu cầu phần mềm"}',
            'tag_name': null,
            'versions': 1,
            'deleted_at': null,
            'created_at': '2023-05-23T01:59:44.000000Z',
            'updated_at': '2023-05-23T01:59:44.000000Z',
            'type': 1,
            'parent_id': null,
            'order': null,
            'explain': '{"en": "Phân tích yêu cầu phần mềm", "ja": "Phân tích yêu cầu phần mềm", "vn": "Phân tích yêu cầu phần mềm"}'
          },
          'max_level': '10',
          'max_score_group': '10',
          'proportion': '10',
          'max_score': '10'
        },
        {
          'id': 129,
          'content': '{"en": "Ước lượng và lập kế hoạch", "ja": "Ước lượng và lập kế hoạch", "vn": "Ước lượng và lập kế hoạch"}',
          'tag_name': null,
          'versions': 1,
          'deleted_at': null,
          'created_at': '2023-05-23T02:00:22.000000Z',
          'updated_at': '2023-05-23T02:00:22.000000Z',
          'type': 1,
          'parent_id': 127,
          'order': null,
          'explain': '{"en": "Ước lượng và lập kế hoạch", "ja": "Ước lượng và lập kế hoạch", "vn": "Ước lượng và lập kế hoạch"}',
          'children_recursive': [],
          'parent': {
            'id': 135,
            'content': '{"en": "Phân tích yêu cầu phần mềm", "ja": "Phân tích yêu cầu phần mềm", "vn": "Phân tích yêu cầu phần mềm"}',
            'tag_name': null,
            'versions': 1,
            'deleted_at': null,
            'created_at': '2023-05-23T01:59:44.000000Z',
            'updated_at': '2023-05-23T01:59:44.000000Z',
            'type': 1,
            'parent_id': null,
            'order': null,
            'explain': '{"en": "Phân tích yêu cầu phần mềm", "ja": "Phân tích yêu cầu phần mềm", "vn": "Phân tích yêu cầu phần mềm"}'
          },
          'categories': [
            {
              'id': 2,
              'name': 'Kĩ năng/Kiến thức',
              'deleted_at': null,
              'created_at': '2023-05-18T09:29:13.000000Z',
              'updated_at': '2023-05-19T10:12:40.000000Z',
              'pivot': {
                'question_id': 129,
                'category_id': 2,
                'created_at': '2023-05-23T02:00:22.000000Z',
                'updated_at': '2023-05-23T02:00:22.000000Z',
                'deleted_at': null
              }
            }
          ],
          'max_level': '10',
          'max_score_group': '10',
          'proportion': '10',
          'max_score': '10'
        },
        {
          'id': 128,
          'content': '{"en": "Phân tích yêu cầu", "ja": "Phân tích yêu cầu", "vn": "Phân tích yêu cầu"}',
          'tag_name': null,
          'versions': 1,
          'deleted_at': null,
          'created_at': '2023-05-23T02:00:08.000000Z',
          'updated_at': '2023-05-23T02:00:08.000000Z',
          'type': 1,
          'parent_id': 133,
          'order': null,
          'explain': '{"en": "Phân tích yêu cầu", "ja": "Phân tích yêu cầu", "vn": "Phân tích yêu cầu"}',
          'children_recursive': [],
          'parent': {
            'id': 134,
            'content': '{"en": "Phân tích yêu cầu phần mềm", "ja": "Phân tích yêu cầu phần mềm", "vn": "Phân tích yêu cầu phần mềm"}',
            'tag_name': null,
            'versions': 1,
            'deleted_at': null,
            'created_at': '2023-05-23T01:59:44.000000Z',
            'updated_at': '2023-05-23T01:59:44.000000Z',
            'type': 1,
            'parent_id': null,
            'order': null,
            'explain': '{"en": "Phân tích yêu cầu phần mềm", "ja": "Phân tích yêu cầu phần mềm", "vn": "Phân tích yêu cầu phần mềm"}'
          },
          'categories': [
            {
              'id': 2,
              'name': 'Kĩ năng/Kiến thức',
              'deleted_at': null,
              'created_at': '2023-05-18T09:29:13.000000Z',
              'updated_at': '2023-05-19T10:12:40.000000Z',
              'pivot': {
                'question_id': 128,
                'category_id': 2,
                'created_at': '2023-05-23T02:00:08.000000Z',
                'updated_at': '2023-05-23T02:00:08.000000Z',
                'deleted_at': null
              }
            }
          ],
          'max_level': '10',
          'max_score_group': '10',
          'proportion': '10',
          'max_score': '10'
        },
        {
          'id': 128,
          'content': '{"en": "Phân tích yêu cầu", "ja": "Phân tích yêu cầu", "vn": "Phân tích yêu cầu"}',
          'tag_name': null,
          'versions': 1,
          'deleted_at': null,
          'created_at': '2023-05-23T02:00:08.000000Z',
          'updated_at': '2023-05-23T02:00:08.000000Z',
          'type': 1,
          'parent_id': 133,
          'order': null,
          'explain': '{"en": "Phân tích yêu cầu", "ja": "Phân tích yêu cầu", "vn": "Phân tích yêu cầu"}',
          'children_recursive': [
          ],
          'parent': {
            'id': 135,
            'content': '{"en": "Phân tích yêu cầu phần mềm", "ja": "Phân tích yêu cầu phần mềm", "vn": "Phân tích yêu cầu phần mềm"}',
            'tag_name': null,
            'versions': 1,
            'deleted_at': null,
            'created_at': '2023-05-23T01:59:44.000000Z',
            'updated_at': '2023-05-23T01:59:44.000000Z',
            'type': 1,
            'parent_id': null,
            'order': null,
            'explain': '{"en": "Phân tích yêu cầu phần mềm", "ja": "Phân tích yêu cầu phần mềm", "vn": "Phân tích yêu cầu phần mềm"}'
          },
          'categories': [
            {
              'id': 2,
              'name': 'Kĩ năng/Kiến thức',
              'deleted_at': null,
              'created_at': '2023-05-18T09:29:13.000000Z',
              'updated_at': '2023-05-19T10:12:40.000000Z',
              'pivot': {
                'question_id': 128,
                'category_id': 2,
                'created_at': '2023-05-23T02:00:08.000000Z',
                'updated_at': '2023-05-23T02:00:08.000000Z',
                'deleted_at': null
              }
            }
          ],
          'max_level': '10',
          'max_score_group': '10',
          'proportion': '10',
          'max_score': '10'
        },
        {
          'id': 128,
          'content': '{"en": "Phân tích yêu cầu", "ja": "Phân tích yêu cầu", "vn": "Phân tích yêu cầu"}',
          'tag_name': null,
          'versions': 1,
          'deleted_at': null,
          'created_at': '2023-05-23T02:00:08.000000Z',
          'updated_at': '2023-05-23T02:00:08.000000Z',
          'type': 1,
          'parent_id': 133,
          'parent': {
            'id': 133,
            'content': '{"en": "Phân tích yêu cầu phần mềm", "ja": "Phân tích yêu cầu phần mềm", "vn": "Phân tích yêu cầu phần mềm"}',
            'tag_name': null,
            'versions': 1,
            'deleted_at': null,
            'created_at': '2023-05-23T01:59:44.000000Z',
            'updated_at': '2023-05-23T01:59:44.000000Z',
            'type': 1,
            'parent_id': null,
            'order': null,
            'explain': '{"en": "Phân tích yêu cầu phần mềm", "ja": "Phân tích yêu cầu phần mềm", "vn": "Phân tích yêu cầu phần mềm"}'
          },
          'order': null,
          'explain': '{"en": "Phân tích yêu cầu", "ja": "Phân tích yêu cầu", "vn": "Phân tích yêu cầu"}',
          'children_recursive': [],
          'categories': [
            {
              'id': 2,
              'name': 'Kĩ năng/Kiến thức',
              'deleted_at': null,
              'created_at': '2023-05-18T09:29:13.000000Z',
              'updated_at': '2023-05-19T10:12:40.000000Z',
              'pivot': {
                'question_id': 128,
                'category_id': 2,
                'created_at': '2023-05-23T02:00:08.000000Z',
                'updated_at': '2023-05-23T02:00:08.000000Z',
                'deleted_at': null
              }
            }
          ],
          'max_level': '10',
          'max_score_group': '10',
          'proportion': '10',
          'max_score': '10'
        },
        {
          'id': 128,
          'content': '{"en": "Phân tích yêu cầu", "ja": "Phân tích yêu cầu", "vn": "Phân tích yêu cầu"}',
          'tag_name': null,
          'versions': 1,
          'deleted_at': null,
          'created_at': '2023-05-23T02:00:08.000000Z',
          'updated_at': '2023-05-23T02:00:08.000000Z',
          'type': 1,
          'parent_id': 133,
          'order': null,
          'explain': '{"en": "Phân tích yêu cầu", "ja": "Phân tích yêu cầu", "vn": "Phân tích yêu cầu"}',
          'children_recursive': [],
          'parent': {
            'id': 136,
            'content': '{"en": "Phân tích yêu cầu phần mềm", "ja": "Phân tích yêu cầu phần mềm", "vn": "Phân tích yêu cầu phần mềm"}',
            'tag_name': null,
            'versions': 1,
            'deleted_at': null,
            'created_at': '2023-05-23T01:59:44.000000Z',
            'updated_at': '2023-05-23T01:59:44.000000Z',
            'type': 1,
            'parent_id': null,
            'order': null,
            'explain': '{"en": "Phân tích yêu cầu phần mềm", "ja": "Phân tích yêu cầu phần mềm", "vn": "Phân tích yêu cầu phần mềm"}'
          },
          'categories': [
            {
              'id': 2,
              'name': 'Kĩ năng/Kiến thức',
              'deleted_at': null,
              'created_at': '2023-05-18T09:29:13.000000Z',
              'updated_at': '2023-05-19T10:12:40.000000Z',
              'pivot': {
                'question_id': 128,
                'category_id': 2,
                'created_at': '2023-05-23T02:00:08.000000Z',
                'updated_at': '2023-05-23T02:00:08.000000Z',
                'deleted_at': null
              }
            }
          ],
          'max_level': '10',
          'max_score_group': '10',
          'proportion': '10',
          'max_score': '10'
        }
      ]
      // caculatePoint: 0
    }
  },
  computed: {
    ...mapGetters([
      'roles'
    ]),
    totalCaculatePoint() {
      if (Object.values(this.yourAnswers) && Object.values(this.yourAnswers).length) {
        return Object.values(this.yourAnswers).reduce((acc, cur) => acc + cur.caculate_point, 0)
      }
      return 0
    }
  },
  created() {
    if (!this.roles.includes('admin')) {
      this.currentRole = 'editorDashboard'
    }
    this.parentAndChildData = this.dataTable.filter((item) => item.children_recursive.length > 0).map((item) => {
      item.children_recursive.map((child) => {
        this.yourAnswers.push({
          id: child.id,
          question_name: JSON.parse(child.content).en,
          parent_id: child.parent_id,
          your_answer: null,
          category_id: child.categories[0].id || null,
          max_level: child.max_level || 5,
          max_score: child.max_score,
          caculate_point: 0,
          note: null
        })
        child['your_answer'] = null
        return child
      })
      return item
    })
    this.yourAnswers = this.yourAnswers.reduce((result, object) => {
      result[`${object.parent_id}_${object.id}`] = object
      return result
    }, {})
  },
  methods: {
    changeAnswer(key) {
      this.yourAnswers[key].caculate_point = (Number(this.yourAnswers[key].your_answer) / Number(this.yourAnswers[key].max_level)) * Number(this.yourAnswers[key].max_score)
    }
  }
}
</script>
<style>
table, th, td {
  border: 1px solid black;
  border-collapse: collapse;
  padding: 10px;
}
.dashboard-container {
  padding: 20px 50px 20px 50px;
}
</style>
