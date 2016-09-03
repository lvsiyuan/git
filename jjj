/**
 * Created by xuwei on 2016/7/5.
 */

bss_wrap.controller("b2b-goodsRelController",["$scope","b2b-viewListNewServices","b2b-serviceHelper",function($scope,viewListNewServices,serviceHelper){
    $scope.data = {};
    $scope.event = {};
    var sourceUrl ={};
    sourceUrl.list = "/bss/goodRel/queryGoodRelsByPage";
    sourceUrl.add = "/bss/goodRel/addGoodRel";
    sourceUrl.edit = "/bss/goodRel/modifyGoodRel";
    sourceUrl.delete = "/bss/goodRel/removeGoodRel";

    /**
     * 流量包管理列表
     */
    $scope.viewList_opt = {
        json:true,
        isApply:true,
        currentPage: 1,
        perPageCount: 10,
        search: {state:$scope.data.state},
        pageShowNums:7,
        url: sourceUrl.list,
        method: "post",
        parton:"baseCode,realCode,realFlag,realType,effDate,expDate,createCustName",
        target:"goodsRel",
        lanName:'goodsRelController',
        keyer:[{
            relate:'realFlag',
            type: {type:"REALFLAG"},
            setValue:"name",
            url: '/bss/dictionary/queryDictionary'
        },
        {
            relate:'realType',
            type: {type:"REALTYPE"},
            setValue:"name",
            url: '/bss/dictionary/queryDictionary'
        }
        ]
    };
    serviceHelper.dictionaryHandleBss({types:"REALFLAG",suc:function(data){
        $scope.data.realFlagList = data;
    }});
    serviceHelper.dictionaryHandleBss({types:"REALTYPE",suc:function(data){
        $scope.data.realTypeList = data;
    }});
    var searchHandle = function(){};
    $scope.$on("viewList_setData",function(e,m){
        searchHandle = m;
    });
    $scope.$on("viewList_currData",function(e,m){
        $scope.data.viewData = m[0];
        $scope.data.selectedId = m[1];
        $scope.data.hideData = m[2];
    });

    $scope.event.search = function(){
        var opt = {
            search:{realFlag :$scope.data.realFlag,baseCode:$scope.data.baseCode,realCode:$scope.data.realCode,realType :$scope.data.realType}
        };
        searchHandle(opt);
    };

    /**
     * 添加销售品关系
     */
    $("#dataView_add_tck form").validate({
        debug: true,
        submitHandler: function (form) {
            var objs={};
            var $from =  $("#dataView_add_tck");
            $from.find("input,select,textarea").each(function(){
                if($(this).attr("name")!=null&&$(this).attr("name")!=undefined&&$(this).attr("name")!="") {
                    objs[$(this).attr("name")] = $(this).val();
                }
            });
            delete objs.bindActive;

            serviceHelper.baseHandleJquery({
                json:true,
                url: sourceUrl.add,
                method: 'post',
                data: objs,
                faildss: function (data) {
                    _msgHelper.showMsgbox({imgUrl: "3", title: _landHelper.lanPackage['common']['errorTips'], content: data.resultDesc, secBtn: false});
                    return;
                },
                suc: function(data){
                    _msgHelper.showMsgbox({imgUrl: "0", title: _landHelper.lanPackage['common']['successTips'], content: data.resultDesc, secBtn: false});
                    $scope.event.search();
                    $("#dataView_add_tck").removeClass("active in")
                }
            });
        }
    });

    $scope.event.edit = function(){
        if($scope.data.hideData == undefined ||  !$scope.data.hideData.id){
            _msgHelper.showMsgbox({imgUrl:"3",title:_landHelper.lanPackage['common']['errorTips'],content:_landHelper.lanPackage['goodsRelController']['selectGoodsRel'], secBtn: false});
            return;
        }
    };

    $scope.event.editSubmit = function(){
        if($scope.data.hideData == undefined ||  !$scope.data.hideData.id){
            _msgHelper.showMsgbox({imgUrl:"3",title:_landHelper.lanPackage['common']['errorTips'],content:_landHelper.lanPackage['goodsRelController']['selectGoodsRel'], secBtn: false});
            return;
        }
        serviceHelper.baseHandleJquery({
            json:true,
            url: sourceUrl.edit,
            method: 'post',
            data: {goodRelId:$scope.data.hideData.id,realType:$("#realType").val()},
            faildss: function (data) {
                _msgHelper.showMsgbox({imgUrl: "3", title: _landHelper.lanPackage['common']['errorTips'], content: data.resultDesc, secBtn: false});
                return;
            },
            suc: function(data){
                _msgHelper.showMsgbox({imgUrl: "0", title: _landHelper.lanPackage['common']['successTips'], content: data.resultDesc, secBtn: false});
                $scope.event.search();
                $("#dataView_edit_tck").removeClass("active in")
            }
        });
    };

    $scope.event.delete = function(){
        if($scope.data.hideData == undefined ||  !$scope.data.hideData.id){
            _msgHelper.showMsgbox({imgUrl:"3",title:_landHelper.lanPackage['common']['errorTips'],content:_landHelper.lanPackage['goodsRelController']['selectGoodsRel'], secBtn: false});
            return;
        }
        _msgHelper.showMsgbox({
            imgUrl:"3",
            title:_landHelper.lanPackage['common']['tips'],
            content:_landHelper.lanPackage['common']['delConfrm'],
            secBtn: true,
            callBack:function(){
                serviceHelper.baseHandleJquery({
                    json:true,
                    url: sourceUrl.delete,
                    method: 'post',
                    data: {goodRelId:$scope.data.hideData.id},
                    faildss: function (data) {
                        _msgHelper.showMsgbox({imgUrl: "3", title: _landHelper.lanPackage['common']['errorTips'], content: data.resultDesc, secBtn: false});
                        return;
                    },
                    suc: function(data){
                        _msgHelper.showMsgbox({imgUrl: "0", title: _landHelper.lanPackage['common']['successTips'], content: _landHelper.lanPackage['common']['delSuccess'], secBtn: false});
                        $scope.event.search();
                    }
                });
            }
        });
    };

}]);
